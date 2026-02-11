import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { motion } from "framer-motion";
import { ShieldCheck, Phone, Mail, MapPin } from "lucide-react";

export default function SilicaFashionsWebsite() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    message: "",
  });

  const [submitted, setSubmitted] = useState(false);

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();

    // Basic frontend validation
    if (!formData.name || !formData.email || !formData.message) {
      alert("Please fill in all fields.");
      return;
    }

    // Email format validation
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(formData.email)) {
      alert("Please enter a valid email address.");
      return;
    }

    // In real production: send to secure backend API (HTTPS, CSRF protection, server-side validation)
    console.log("Secure form submission:", formData);
    setSubmitted(true);
    setFormData({ name: "", email: "", message: "" });
  };

  return (
    <div className="min-h-screen bg-gray-50 text-gray-800">
      {/* Header */}
      <header className="bg-white shadow-md sticky top-0 z-50">
        <div className="max-w-7xl mx-auto flex justify-between items-center p-4">
          <h1 className="text-2xl font-bold">Silica Fashions</h1>
          <nav className="space-x-6 text-sm font-medium">
            <a href="#about" className="hover:text-black">About</a>
            <a href="#services" className="hover:text-black">Collections</a>
            <a href="#contact" className="hover:text-black">Contact</a>
          </nav>
        </div>
      </header>

      {/* Hero Section */}
      <section className="bg-gradient-to-r from-gray-900 to-gray-700 text-white py-20">
        <div className="max-w-7xl mx-auto text-center px-6">
          <motion.h2
            initial={{ opacity: 0, y: -20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.8 }}
            className="text-4xl md:text-5xl font-bold mb-6"
          >
            Premium Fashion. Professional Elegance.
          </motion.h2>
          <p className="max-w-2xl mx-auto text-lg mb-8">
            Silica Fashions delivers high-quality, stylish, and modern clothing tailored for confidence and excellence.
          </p>
          <Button className="rounded-2xl px-8 py-3 text-base">Shop Collection</Button>
        </div>
      </section>

      {/* About Section */}
      <section id="about" className="py-16 px-6 max-w-6xl mx-auto">
        <h3 className="text-3xl font-bold text-center mb-8">About Silica Fashions</h3>
        <p className="text-center text-lg max-w-3xl mx-auto">
          Based in Eldoret, Silica Fashions is committed to providing dependable and professional fashion solutions.
          We combine quality materials, modern designs, and exceptional customer service to meet business and personal fashion needs.
        </p>
      </section>

      {/* Services / Collections */}
      <section id="services" className="py-16 bg-white">
        <div className="max-w-6xl mx-auto px-6 grid md:grid-cols-3 gap-8">
          {["Corporate Wear", "Casual Collections", "Custom Designs"].map((item, index) => (
            <motion.div
              key={index}
              whileHover={{ scale: 1.05 }}
              transition={{ duration: 0.3 }}
            >
              <Card className="rounded-2xl shadow-lg">
                <CardContent className="p-6 text-center">
                  <h4 className="text-xl font-semibold mb-4">{item}</h4>
                  <p>
                    High-quality materials, professional finishing, and dependable service tailored to your needs.
                  </p>
                </CardContent>
              </Card>
            </motion.div>
          ))}
        </div>
      </section>

      {/* Contact Section */}
      <section id="contact" className="py-16 bg-gray-100">
        <div className="max-w-6xl mx-auto px-6 grid md:grid-cols-2 gap-12">
          <div>
            <h3 className="text-3xl font-bold mb-6">Contact Us</h3>
            <div className="space-y-4 text-lg">
              <p className="flex items-center gap-3"><Phone size={20} /> 0707-452-491</p>
              <p className="flex items-center gap-3"><Mail size={20} /> samuelcharo724@gmail.com</p>
              <p className="flex items-center gap-3"><MapPin size={20} /> Eldoret</p>
              <p className="flex items-center gap-3"><ShieldCheck size={20} /> Secure & Professional Service</p>
            </div>
          </div>

          <Card className="rounded-2xl shadow-xl">
            <CardContent className="p-6">
              <form onSubmit={handleSubmit} className="space-y-4">
                <Input
                  type="text"
                  name="name"
                  placeholder="Your Name"
                  value={formData.name}
                  onChange={handleChange}
                  required
                />
                <Input
                  type="email"
                  name="email"
                  placeholder="Your Email"
                  value={formData.email}
                  onChange={handleChange}
                  required
                />
                <Textarea
                  name="message"
                  placeholder="Your Message"
                  value={formData.message}
                  onChange={handleChange}
                  required
                />
                <Button type="submit" className="w-full rounded-2xl">Send Message</Button>
                {submitted && (
                  <p className="text-green-600 text-sm mt-2">Message submitted successfully!</p>
                )}
              </form>
            </CardContent>
          </Card>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-white py-6 text-center text-sm">
        © {new Date().getFullYear()} Silica Fashions. All rights reserved. | Professional & Secure Fashion Business
      </footer>
    </div>
  );
}

