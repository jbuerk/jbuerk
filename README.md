- 👋 Hi, I’m @jbuerk
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
jbuerk/jbuerk is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Brain, CheckCircle, School, Clock, MessageSquare, Star, X, Send, ChevronDown } from 'lucide-react';
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog";

// Custom FAQ Accordion Component
const FAQItem = ({ question, answer }) => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div className="border-b border-gray-200">
      <button
        className="w-full py-4 px-6 flex justify-between items-center hover:bg-gray-50"
        onClick={() => setIsOpen(!isOpen)}
      >
        <span className="font-medium text-left">{question}</span>
        <ChevronDown 
          className={`h-5 w-5 transition-transform duration-200 ${
            isOpen ? 'transform rotate-180' : ''
          }`}
        />
      </button>
      <div
        className={`overflow-hidden transition-all duration-200 ${
          isOpen ? 'max-h-48' : 'max-h-0'
        }`}
      >
        <div className="p-6 bg-gray-50">{answer}</div>
      </div>
    </div>
  );
};

const MentalHealthCoach = () => {
  const [selectedPlan, setSelectedPlan] = useState(null);
  const [showChat, setShowChat] = useState(false);
  const [messages, setMessages] = useState([
    { text: "Hi! I'm your AI mental health coach. How are you feeling today?", sender: 'ai' }
  ]);
  const [newMessage, setNewMessage] = useState('');
  const [email, setEmail] = useState('');
  
  const plans = [
    {
      name: 'Basic Plan',
      price: 29.99,
      features: [
        '4 AI coaching sessions per month',
        '30-minute session duration',
        'Basic mood tracking',
        'Text-based chat support',
        'Guided meditation library'
      ]
    },
    {
      name: 'Premium Plan',
      price: 49.99,
      features: [
        'Unlimited AI coaching sessions',
        '60-minute session duration',
        'Advanced mood & habit tracking',
        'Priority 24/7 chat support',
        'Full wellness resource library',
        'Progress analytics dashboard',
        'Personalized action plans'
      ]
    }
  ];

  const faqs = [
    {
      question: "How does AI mental health coaching work?",
      answer: "Our AI coach uses advanced natural language processing to provide personalized support, guidance, and coping strategies. It's available 24/7 and learns from your interactions to offer more tailored assistance over time."
    },
    {
      question: "Is my data private and secure?",
      answer: "Yes, we take privacy very seriously. All conversations are encrypted, and we comply with HIPAA and other relevant data protection regulations. Your information is never shared without your explicit consent."
    },
    {
      question: "Can AI coaching replace traditional therapy?",
      answer: "While our AI coach provides valuable support and coping strategies, it's not a replacement for professional therapy. We recommend using it as a complementary tool and seeking professional help when needed."
    }
  ];

  const handleSendMessage = () => {
    if (newMessage.trim()) {
      setMessages([...messages, { text: newMessage, sender: 'user' }]);
      // Simulate AI response
      setTimeout(() => {
        setMessages(prev => [...prev, {
          text: "I understand how you're feeling. Let's work through this together. Would you like to try some breathing exercises or talk more about what's on your mind?",
          sender: 'ai'
        }]);
      }, 1000);
      setNewMessage('');
    }
  };

  const handleTryDemo = () => {
    setShowChat(true);
  };

  const handlePlanSelect = (planName) => {
    setSelectedPlan(planName);
  };

  // Rest of the component remains the same until the FAQ section
  return (
    <div className="min-h-screen bg-gray-50">
      {/* Previous sections remain unchanged */}
      
      {/* Hero Section */}
      <div className="bg-blue-600 text-white py-16">
        <div className="max-w-4xl mx-auto px-4 text-center">
          <Brain className="mx-auto mb-6 h-16 w-16" />
          <h1 className="text-4xl font-bold mb-4">MindMentor.AI</h1>
          <p className="text-xl mb-8">Your Personal AI Mental Health Coach for College Success</p>
          <div className="flex justify-center space-x-4">
            <Dialog>
              <DialogTrigger asChild>
                <Button className="bg-white text-blue-600 hover:bg-gray-100">Get Started</Button>
              </DialogTrigger>
              <DialogContent>
                <DialogHeader>
                  <DialogTitle>Start Your Journey</DialogTitle>
                </DialogHeader>
                <div className="space-y-4 p-4">
                  <Input
                    type="email"
                    placeholder="Enter your email"
                    value={email}
                    onChange={(e) => setEmail(e.target.value)}
                  />
                  <Button className="w-full" onClick={() => alert("Thank you! We'll be in touch soon.")}>
                    Sign Up
                  </Button>
                </div>
              </DialogContent>
            </Dialog>
            <Button variant="outline" className="border-white text-white hover:bg-blue-700" onClick={handleTryDemo}>
              Try Demo
            </Button>
          </div>
        </div>
      </div>

      {/* Chat Demo */}
      {showChat && (
        <div className="fixed bottom-4 right-4 w-96 h-96 bg-white rounded-lg shadow-xl flex flex-col">
          <div className="p-4 bg-blue-600 text-white rounded-t-lg flex justify-between items-center">
            <h3 className="font-bold">AI Coach Demo</h3>
            <Button variant="ghost" className="text-white h-6 w-6 p-0" onClick={() => setShowChat(false)}>
              <X className="h-4 w-4" />
            </Button>
          </div>
          <div className="flex-1 p-4 overflow-y-auto space-y-4">
            {messages.map((message, index) => (
              <div
                key={index}
                className={`flex ${message.sender === 'user' ? 'justify-end' : 'justify-start'}`}
              >
                <div
                  className={`p-3 rounded-lg max-w-[80%] ${
                    message.sender === 'user'
                      ? 'bg-blue-600 text-white'
                      : 'bg-gray-100 text-gray-900'
                  }`}
                >
                  {message.text}
                </div>
              </div>
            ))}
          </div>
          <div className="p-4 border-t flex gap-2">
            <Input
              value={newMessage}
              onChange={(e) => setNewMessage(e.target.value)}
              placeholder="Type your message..."
              onKeyPress={(e) => e.key === 'Enter' && handleSendMessage()}
            />
            <Button onClick={handleSendMessage}>
              <Send className="h-4 w-4" />
            </Button>
          </div>
        </div>
      )}

      {/* Benefits Section */}
      <div className="max-w-6xl mx-auto py-16 px-4">
        <h2 className="text-3xl font-bold text-center mb-12">Why Choose MindMentor.AI?</h2>
        <div className="grid md:grid-cols-3 gap-8">
          <Card className="text-center p-6 hover:shadow-lg transition-shadow duration-300">
            <Clock className="mx-auto h-12 w-12 text-blue-600 mb-4" />
            <CardTitle className="mb-4">24/7 Availability</CardTitle>
            <p>Get support whenever you need it, fitting your busy student schedule</p>
          </Card>
          <Card className="text-center p-6 hover:shadow-lg transition-shadow duration-300">
            <MessageSquare className="mx-auto h-12 w-12 text-blue-600 mb-4" />
            <CardTitle className="mb-4">Personalized Support</CardTitle>
            <p>AI-powered conversations tailored to your unique needs and goals</p>
          </Card>
          <Card className="text-center p-6 hover:shadow-lg transition-shadow duration-300">
            <School className="mx-auto h-12 w-12 text-blue-600 mb-4" />
            <CardTitle className="mb-4">Student-Focused</CardTitle>
            <p>Designed specifically for college life challenges and stress management</p>
          </Card>
        </div>
      </div>

      {/* Pricing Section */}
      <div className="bg-gray-100 py-16 px-4">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-3xl font-bold text-center mb-12">Choose Your Plan</h2>
          <div className="grid md:grid-cols-2 gap-8">
            {plans.map((plan) => (
              <Card 
                key={plan.name}
                className={`relative transform transition-all duration-300 hover:scale-105 ${
                  selectedPlan === plan.name ? 'border-blue-600 border-2' : ''
                }`}
              >
                <CardHeader>
                  <CardTitle className="flex justify-between items-center">
                    <span>{plan.name}</span>
                    <span className="text-2xl font-bold">${plan.price}/month</span>
                  </CardTitle>
                </CardHeader>
                <CardContent>
                  <ul className="space-y-4">
                    {plan.features.map((feature) => (
                      <li key={feature} className="flex items-center">
                        <CheckCircle className="h-5 w-5 text-green-500 mr-2" />
                        {feature}
                      </li>
                    ))}
                  </ul>
                  <Button 
                    className="w-full mt-6"
                    variant={plan.name === 'Premium Plan' ? 'default' : 'outline'}
                    onClick={() => handlePlanSelect(plan.name)}
                  >
                    {selectedPlan === plan.name ? 'Selected' : 'Select Plan'}
                  </Button>
                </CardContent>
                {plan.name === 'Premium Plan' && (
                  <div className="absolute -top-4 right-4 bg-blue-600 text-white px-4 py-1 rounded-full flex items-center">
                    <Star className="h-4 w-4 mr-1" />
                    Most Popular
                  </div>
                )}
              </Card>
            ))}
          </div>
        </div>
      </div>

      {/* FAQ Section - Now using custom accordion */}
      <div className="max-w-4xl mx-auto py-16 px-4">
        <h2 className="text-3xl font-bold text-center mb-12">Frequently Asked Questions</h2>
        <div className="rounded-lg border border-gray-200 divide-y">
          {faqs.map((faq, index) => (
            <FAQItem key={index} question={faq.question} answer={faq.answer} />
          ))}
        </div>
      </div>

      {/* CTA Section */}
      <div className="bg-blue-600 text-white py-16 px-4">
        <div className="max-w-4xl mx-auto text-center">
          <h2 className="text-3xl font-bold mb-4">For Universities</h2>
          <p className="text-xl mb-8">
            Partner with us to provide mental health support for your entire student body.
            Custom pricing and integration available for educational institutions.
          </p>
          <Dialog>
            <DialogTrigger asChild>
              <Button className="bg-white text-blue-600 hover:bg-gray-100">
                Contact for Partnership
              </Button>
            </DialogTrigger>
            <DialogContent>
              <DialogHeader>
                <DialogTitle>Partner With Us</DialogTitle>
              </DialogHeader>
              <div className="space-y-4 p-4">
                <Input placeholder="Institution Name" />
                <Input placeholder="Contact Email" />
                <Button className="w-full" onClick={() => alert("Thank you for your interest! We'll be in touch soon.")}>
                  Submit
                </Button>
              </div>
            </DialogContent>
          </Dialog>
        </div>
      </div>
    </div>
  );
};

export default MentalHealthCoach;

Version 3 of 3
