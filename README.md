"use client";

import { useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { 
  Menu, 
  X, 
  Download, 
  Mail, 
  MapPin, 
  Instagram, 
  Youtube, 
  Twitter, 
  Linkedin,
  FileText,
  Image,
  Video,
  Palette,
  User,
  ShoppingBag,
  BookOpen
} from "lucide-react";

export default function CynicalGirlWebsite() {
  const [activeSection, setActiveSection] = useState("inicio");
  const [isMenuOpen, setIsMenuOpen] = useState(false);

  const navigationItems = [
    { id: "inicio", label: "Inicio", icon: null },
    { id: "sobre-mi", label: "Sobre Mí", icon: User },
    { id: "portafolios", label: "Portafolios", icon: FileText },
    { id: "mediakit", label: "Mediakit", icon: Download },
    { id: "servicios", label: "Servicios", icon: Palette },
    { id: "tienda", label: "Tienda", icon: ShoppingBag },
    { id: "blog", label: "Blog", icon: BookOpen },
    { id: "contacto", label: "Contacto", icon: Mail },
  ];

  const socialMedia = [
    { platform: "Instagram", url: "#", icon: Instagram },
    { platform: "YouTube", url: "#", icon: Youtube },
    { platform: "Twitter", url: "#", icon: Twitter },
    { platform: "LinkedIn", url: "#", icon: Linkedin },
  ];

  const renderSection = () => {
    switch (activeSection) {
      case "inicio":
        return <HomeSection />;
      case "sobre-mi":
        return <AboutSection />;
      case "portafolios":
        return <PortfoliosSection />;
      case "mediakit":
        return <MediakitSection />;
      case "servicios":
        return <ServicesSection />;
      case "tienda":
        return <ShopSection />;
      case "blog":
        return <BlogSection />;
      case "contacto":
        return <ContactSection />;
      default:
        return <HomeSection />;
    }
  };

  return (
    <div className="min-h-screen bg-white text-gray-900">
      {/* Header */}
      <header className="fixed top-0 w-full bg-white/95 backdrop-blur-sm z-50 border-b border-gray-200">
        <div className="container mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between items-center h-16">
            {/* Logo */}
            <motion.div 
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              className="flex items-center"
            >
              <h1 className="text-2xl font-bold text-red-600">CynicalGirl</h1>
            </motion.div>

            {/* Desktop Navigation */}
            <nav className="hidden md:flex space-x-8">
              {navigationItems.map((item) => (
                <motion.button
                  key={item.id}
                  whileHover={{ scale: 1.05 }}
                  whileTap={{ scale: 0.95 }}
                  onClick={() => setActiveSection(item.id)}
                  className={`px-3 py-2 rounded-md text-sm font-medium transition-colors ${
                    activeSection === item.id
                      ? "text-red-600 border-b-2 border-red-600"
                      : "text-gray-700 hover:text-red-600"
                  }`}
                >
                  {item.label}
                </motion.button>
              ))}
            </nav>

            {/* Mobile Menu Button */}
            <button
              className="md:hidden text-gray-700"
              onClick={() => setIsMenuOpen(!isMenuOpen)}
            >
              {isMenuOpen ? <X size={24} /> : <Menu size={24} />}
            </button>
          </div>
        </div>
      </header>

      {/* Mobile Menu */}
      <AnimatePresence>
        {isMenuOpen && (
          <motion.div
            initial={{ opacity: 0, y: -20 }}
            animate={{ opacity: 1, y: 0 }}
            exit={{ opacity: 0, y: -20 }}
            className="fixed inset-0 z-40 bg-white md:hidden mt-16"
          >
            <div className="px-4 pt-8 pb-4 space-y-4">
              {navigationItems.map((item) => (
                <motion.button
                  key={item.id}
                  whileHover={{ scale: 1.02 }}
                  whileTap={{ scale: 0.98 }}
                  onClick={() => {
                    setActiveSection(item.id);
                    setIsMenuOpen(false);
                  }}
                  className={`w-full flex items-center px-4 py-3 rounded-lg text-left ${
                    activeSection === item.id
                      ? "bg-red-50 text-red-600"
                      : "text-gray-700 hover:bg-gray-50"
                  }`}
                >
                  {item.icon && <item.icon className="mr-3 h-5 w-5" />}
                  <span className="font-medium">{item.label}</span>
                </motion.button>
              ))}
            </div>
          </motion.div>
        )}
      </AnimatePresence>

      {/* Main Content */}
      <main className="pt-16 min-h-screen">
        <AnimatePresence mode="wait">
          <motion.div
            key={activeSection}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            exit={{ opacity: 0, y: -20 }}
            transition={{ duration: 0.3 }}
            className="container mx-auto px-4 sm:px-6 lg:px-8 py-8"
          >
            {renderSection()}
          </motion.div>
        </AnimatePresence>
      </main>

      {/* Footer */}
      <footer className="bg-gray-50 border-t border-gray-200">
        <div className="container mx-auto px-4 sm:px-6 lg:px-8 py-12">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div>
              <h3 className="text-lg font-semibold text-gray-900 mb-4">CynicalGirl</h3>
              <p className="text-gray-600">Creadora de contenido multifacética</p>
              <div className="flex space-x-4 mt-4">
                {socialMedia.map((social) => (
                  <motion.a
                    key={social.platform}
                    href={social.url}
                    whileHover={{ scale: 1.1 }}
                    className="text-gray-600 hover:text-red-600"
                  >
                    <social.icon className="h-5 w-5" />
                  </motion.a>
                ))}
              </div>
            </div>

            <div>
              <h4 className="text-sm font-semibold text-gray-900 uppercase tracking-wider mb-4">
                Ubicación
              </h4>
              <div className="flex items-center text-gray-600">
                <MapPin className="h-5 w-5 mr-2" />
                <span>Ciudad de Panamá, Panamá</span>
              </div>
            </div>

            <div>
              <h4 className="text-sm font-semibold text-gray-900 uppercase tracking-wider mb-4">
                Contacto
              </h4>
              <a
                href="mailto:hola@cynicalgirl.com"
                className="text-red-600 hover:text-red-700 flex items-center"
              >
                <Mail className="h-5 w-5 mr-2" />
                hola@cynicalgirl.com
              </a>
            </div>
          </div>

          <div className="mt-8 pt-8 border-t border-gray-200">
            <p className="text-center text-gray-500 text-sm">
              © {new Date().getFullYear()} CynicalGirl. Todos los derechos reservados.
            </p>
          </div>
        </div>
      </footer>
    </div>
  );
}

// Home Section Component
function HomeSection() {
  return (
    <section className="py-20">
      <div className="max-w-4xl mx-auto text-center">
        <motion.h1
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          className="text-4xl md:text-6xl font-bold text-gray-900 mb-6"
        >
          Hola, soy <span className="text-red-600">CynicalGirl</span>
        </motion.h1>
        
        <motion.p
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ delay: 0.1 }}
          className="text-xl text-gray-600 mb-8 max-w-2xl mx-auto"
        >
          Creadora de contenido, diseñadora gráfica, ilustradora de moda y modelo. 
          Bienvenido a mi mundo creativo.
        </motion.p>

        <motion.div
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ delay: 0.2 }}
          className="flex flex-col sm:flex-row gap-4 justify-center"
        >
          <motion.button
            whileHover={{ scale: 1.05 }}
            whileTap={{ scale: 0.95 }}
            className="bg-red-600 text-white px-8 py-3 rounded-lg font-medium hover:bg-red-700 transition-colors"
          >
            Ver Portafolios
          </motion.button>
          <motion.button
            whileHover={{ scale: 1.05 }}
            whileTap={{ scale: 0.95 }}
            className="border-2 border-gray-300 text-gray-700 px-8 py-3 rounded-lg font-medium hover:border-red-600 hover:text-red-600 transition-colors"
          >
            Contactar
          </motion.button>
        </motion.div>
      </div>
    </section>
  );
}

// About Section Component
function AboutSection() {
  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Sobre Mí</h2>
      
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <div>
          <motion.div
            initial={{ opacity: 0, x: -20 }}
            animate={{ opacity: 1, x: 0 }}
            className="mb-8"
          >
            <h3 className="text-xl font-semibold text-gray-900 mb-4">Introducción</h3>
            <p className="text-gray-600 leading-relaxed">
              Soy una creadora de contenido multifacética con pasión por el diseño, 
              la moda y la expresión creativa. Mi trabajo combina técnicas tradicionales 
              con enfoques digitales modernos para crear contenido auténtico y engaging.
            </p>
          </motion.div>

          <motion.div
            initial={{ opacity: 0, x: -20 }}
            animate={{ opacity: 1, x: 0 }}
            transition={{ delay: 0.1 }}
          >
            <h3 className="text-xl font-semibold text-gray-900 mb-4">Habilidades</h3>
            <div className="space-y-2">
              {["Diseño Gráfico", "Ilustración de Moda", "Creación de Contenido", "Modelaje", "Fotografía", "Edición de Video"].map((skill, index) => (
                <motion.div
                  key={skill}
                  initial={{ opacity: 0, x: -20 }}
                  animate={{ opacity: 1, x: 0 }}
                  transition={{ delay: 0.1 + index * 0.05 }}
                  className="flex items-center"
                >
                  <div className="w-2 h-2 bg-red-600 rounded-full mr-3"></div>
                  <span className="text-gray-600">{skill}</span>
                </motion.div>
              ))}
            </div>
          </motion.div>
        </div>

        <div className="space-y-6">
          <motion.div
            initial={{ opacity: 0, x: 20 }}
            animate={{ opacity: 1, x: 0 }}
            className="bg-gray-50 p-6 rounded-lg"
          >
            <h3 className="text-xl font-semibold text-gray-900 mb-4">Currículum</h3>
            <button className="flex items-center text-red-600 hover:text-red-700">
              <Download className="h-5 w-5 mr-2" />
              Descargar CV
            </button>
          </motion.div>

          <motion.div
            initial={{ opacity: 0, x: 20 }}
            animate={{ opacity: 1, x: 0 }}
            transition={{ delay: 0.1 }}
            className="bg-gray-50 p-6 rounded-lg"
          >
            <h3 className="text-xl font-semibold text-gray-900 mb-4">Compcard</h3>
            <button className="flex items-center text-red-600 hover:text-red-700">
              <Download className="h-5 w-5 mr-2" />
              Descargar Compcard
            </button>
          </motion.div>
        </div>
      </div>
    </section>
  );
}

// Portfolios Section Component
function PortfoliosSection() {
  const portfolios = [
    {
      title: "Diseño Gráfico",
      icon: Palette,
      description: "Proyectos de branding, diseño editorial y gráficos para redes sociales",
      count: "24 proyectos"
    },
    {
      title: "Creadora de Contenido",
      icon: Video,
      description: "Contenido para redes sociales, blogs y plataformas digitales",
      count: "18 proyectos"
    },
    {
      title: "Ilustración de Moda",
      icon: Image,
      description: "Ilustraciones de moda, diseños de prendas y conceptos visuales",
      count: "12 proyectos"
    },
    {
      title: "Modelaje",
      icon: User,
      description: "Portafolio fotográfico y trabajos de modelaje profesional",
      count: "8 proyectos"
    }
  ];

  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Portafolios</h2>
      
      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        {portfolios.map((portfolio, index) => (
          <motion.div
            key={portfolio.title}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: index * 0.1 }}
            whileHover={{ y: -5 }}
            className="bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-shadow cursor-pointer"
          >
            <div className="flex items-center mb-4">
              <div className="w-12 h-12 bg-red-50 rounded-lg flex items-center justify-center mr-4">
                <portfolio.icon className="h-6 w-6 text-red-600" />
              </div>
              <h3 className="text-xl font-semibold text-gray-900">{portfolio.title}</h3>
            </div>
            
            <p className="text-gray-600 mb-4">{portfolio.description}</p>
            
            <div className="flex justify-between items-center">
              <span className="text-sm text-gray-500">{portfolio.count}</span>
              <button className="text-red-600 hover:text-red-700 text-sm font-medium">
                Ver proyectos →
              </button>
            </div>
          </motion.div>
        ))}
      </div>
    </section>
  );
}

// Mediakit Section Component
function MediakitSection() {
  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Mediakit</h2>
      
      <div className="bg-gray-50 rounded-lg p-8">
        <div className="max-w-2xl mx-auto text-center">
          <div className="w-20 h-20 bg-red-100 rounded-full flex items-center justify-center mx-auto mb-6">
            <Download className="h-10 w-10 text-red-600" />
          </div>
          
          <h3 className="text-2xl font-semibold text-gray-900 mb-4">
            Kit de Prensa y Colaboraciones
          </h3>
          
          <p className="text-gray-600 mb-6">
            Descarga mi mediakit completo con estadísticas de audiencia, 
            tarifas de colaboración y portfolio de trabajos anteriores.
          </p>
          
          <motion.button
            whileHover={{ scale: 1.05 }}
            whileTap={{ scale: 0.95 }}
            className="bg-red-600 text-white px-8 py-3 rounded-lg font-medium hover:bg-red-700 transition-colors"
          >
            Descargar Mediakit
          </motion.button>
          
          <p className="text-sm text-gray-500 mt-4">
            Actualizado: {new Date().toLocaleDateString('es-ES', { 
              year: 'numeric', 
              month: 'long', 
              day: 'numeric' 
            })}
          </p>
        </div>
      </div>
    </section>
  );
}

// Services Section Component
function ServicesSection() {
  const services = [
    {
      category: "Diseño Gráfico",
      packages: [
        { name: "Básico", price: "$150", features: ["Logo design", "Brand guidelines", "2 revisiones"] },
        { name: "Premium", price: "$350", features: ["Branding completo", "Manual de marca", "5 revisiones", "Soporte 1 mes"] }
      ]
    },
    {
      category: "Modelaje",
      packages: [
        { name: "Sesión básica", price: "$200", features: ["2 horas de sesión", "5 looks", "10 fotos editadas"] },
        { name: "Pack profesional", price: "$500", features: ["4 horas de sesión", "8 looks", "25 fotos editadas", "Book digital"] }
      ]
    },
    {
      category: "Ilustración",
      packages: [
        { name: "Ilustración simple", price: "$80", features: ["1 ilustración", "Formato digital", "2 revisiones"] },
        { name: "Serie ilustrada", price: "$250", features: ["4 ilustraciones", "Estilo consistente", "Concept development"] }
      ]
    },
    {
      category: "Contenido",
      packages: [
        { name: "Post único", price: "$120", features: ["Content creation", "1 plataforma", "Edición profesional"] },
        { name: "Pack mensual", price: "$800", features: ["12 posts mensuales", "3 plataformas", "Estrategia de contenido", "Analytics"] }
      ]
    }
  ];

  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Servicios</h2>
      
      <div className="space-y-12">
        {services.map((service, index) => (
          <motion.div
            key={service.category}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: index * 0.1 }}
          >
            <h3 className="text-2xl font-semibold text-gray-900 mb-6">{service.category}</h3>
            
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
              {service.packages.map((pkg, pkgIndex) => (
                <motion.div
                  key={pkg.name}
                  whileHover={{ y: -5 }}
                  className="bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-shadow"
                >
                  <h4 className="text-xl font-semibold text-gray-900 mb-2">{pkg.name}</h4>
                  <div className="text-2xl font-bold text-red-600 mb-4">{pkg.price}</div>
                  
                  <ul className="space-y-2 mb-6">
                    {pkg.features.map((feature) => (
                      <li key={feature} className="flex items-center">
                        <div className="w-2 h-2 bg-red-600 rounded-full mr-3"></div>
                        <span className="text-gray-600">{feature}</span>
                      </li>
                    ))}
                  </ul>
                  
                  <button className="w-full bg-red-600 text-white py-2 rounded hover:bg-red-700 transition-colors">
                    Solicitar
                  </button>
                </motion.div>
              ))}
            </div>
          </motion.div>
        ))}
      </div>
    </section>
  );
}

// Shop Section Component
function ShopSection() {
  const digitalProducts = [
    { name: "Presets Lightroom", price: "$25", description: "Pack de 10 presets profesionales" },
    { name: "Plantillas Instagram", price: "$35", description: "20 plantillas editables" },
    { name: "Guía Content Creation", price: "$45", description: "Estrategias probadas para redes" }
  ];

  const merchProducts = [
    { name: "Camiseta Premium", price: "$30", description: "Algodón orgánico, diseño exclusivo" },
    { name: "Taza CynicalGirl", price: "$18", description: "Cerámica de alta calidad" },
    { name: "Poster Ilustrado", price: "$25", description: "Impresión premium, edición limitada" }
  ];

  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Tienda</h2>
      
      <div className="mb-16">
        <h3 className="text-2xl font-semibold text-gray-900 mb-6">Productos Digitales</h3>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          {digitalProducts.map((product, index) => (
            <motion.div
              key={product.name}
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: index * 0.1 }}
              whileHover={{ y: -5 }}
              className="bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-shadow"
            >
              <div className="w-full h-48 bg-gray-100 rounded mb-4 flex items-center justify-center">
                <ShoppingBag className="h-12 w-12 text-gray-400" />
              </div>
              <h4 className="text-lg font-semibold text-gray-900 mb-2">{product.name}</h4>
              <p className="text-gray-600 mb-4">{product.description}</p>
              <div className="flex justify-between items-center">
                <span className="text-xl font-bold text-red-600">{product.price}</span>
                <button className="bg-red-600 text-white px-4 py-2 rounded hover:bg-red-700 transition-colors">
                  Comprar
                </button>
              </div>
            </motion.div>
          ))}
        </div>
      </div>

      <div>
        <h3 className="text-2xl font-semibold text-gray-900 mb-6">Merchandising</h3>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          {merchProducts.map((product, index) => (
            <motion.div
              key={product.name}
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: index * 0.1 }}
              whileHover={{ y: -5 }}
              className="bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-shadow"
            >
              <div className="w-full h-48 bg-gray-100 rounded mb-4 flex items-center justify-center">
                <ShoppingBag className="h-12 w-12 text-gray-400" />
              </div>
              <h4 className="text-lg font-semibold text-gray-900 mb-2">{product.name}</h4>
              <p className="text-gray-600 mb-4">{product.description}</p>
              <div className="flex justify-between items-center">
                <span className="text-xl font-bold text-red-600">{product.price}</span>
                <button className="bg-red-600 text-white px-4 py-2 rounded hover:bg-red-700 transition-colors">
                  Comprar
                </button>
              </div>
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}

// Blog Section Component
function BlogSection() {
  const blogPosts = [
    {
      title: "Mi journey como creadora de contenido",
      excerpt: "Cómo empecé en el mundo del content creation y los lessons learned...",
      date: "15 Nov 2024",
      category: "Experiencias"
    },
    {
      title: "Guía completa de ilustración de moda digital",
      excerpt: "Técnicas y herramientas para crear ilustraciones de moda profesionales...",
      date: "8 Nov 2024",
      category: "Tutoriales"
    },
    {
      title: "Behind the scenes: Sesión de modelaje profesional",
      excerpt: "Todo lo que necesitas saber para prepararte para una sesión de fotos...",
      date: "1 Nov 2024",
      category: "Behind the Scenes"
    }
  ];

  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Blog</h2>
      
      <div className="space-y-8">
        {blogPosts.map((post, index) => (
          <motion.article
            key={post.title}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ delay: index * 0.1 }}
            whileHover={{ y: -5 }}
            className="bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-shadow cursor-pointer"
          >
            <span className="inline-block bg-red-100 text-red-800 text-sm font-medium px-3 py-1 rounded-full mb-4">
              {post.category}
            </span>
            
            <h3 className="text-xl font-semibold text-gray-900 mb-3">{post.title}</h3>
            
            <p className="text-gray-600 mb-4">{post.excerpt}</p>
            
            <div className="flex justify-between items-center">
              <time className="text-sm text-gray-500">{post.date}</time>
              <button className="text-red-600 hover:text-red-700 text-sm font-medium">
                Leer más →
              </button>
            </div>
          </motion.article>
        ))}
      </div>
    </section>
  );
}

// Contact Section Component
function ContactSection() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    subject: "",
    message: ""
  });

  const handleInputChange = (e: React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement>) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    // Handle form submission
    console.log("Form submitted:", formData);
  };

  return (
    <section className="py-12">
      <h2 className="text-3xl font-bold text-gray-900 mb-8">Contacto</h2>
      
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <div>
          <h3 className="text-xl font-semibold text-gray-900 mb-6">Envíame un mensaje</h3>
          
          <form onSubmit={handleSubmit} className="space-y-6">
            <div>
              <label htmlFor="name" className="block text-sm font-medium text-gray-700 mb-2">
                Nombre
              </label>
              <input
                type="text"
                id="name"
                name="name"
                value={formData.name}
                onChange={handleInputChange}
                className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-600 focus:border-transparent"
                required
              />
            </div>
            
            <div>
              <label htmlFor="email" className="block text-sm font-medium text-gray-700 mb-2">
                Email
              </label>
              <input
                type="email"
                id="email"
                name="email"
                value={formData.email}
                onChange={handleInputChange}
                className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-600 focus:border-transparent"
                required
              />
            </div>
            
            <div>
              <label htmlFor="subject" className="block text-sm font-medium text-gray-700 mb-2">
                Asunto
              </label>
              <input
                type="text"
                id="subject"
                name="subject"
                value={formData.subject}
                onChange={handleInputChange}
                className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-600 focus:border-transparent"
                required
              />
            </div>
            
            <div>
              <label htmlFor="message" className="block text-sm font-medium text-gray-700 mb-2">
                Mensaje
              </label>
              <textarea
                id="message"
                name="message"
                rows={5}
                value={formData.message}
                onChange={handleInputChange}
                className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-600 focus:border-transparent"
                required
              />
            </div>
            
            <motion.button
              whileHover={{ scale: 1.02 }}
              whileTap={{ scale: 0.98 }}
              type="submit"
              className="w-full bg-red-600 text-white py-3 rounded-lg font-medium hover:bg-red-700 transition-colors"
            >
              Enviar Mensaje
            </motion.button>
          </form>
        </div>
        
        <div>
          <h3 className="text-xl font-semibold text-gray-900 mb-6">Información de Contacto</h3>
          
          <div className="space-y-6">
            <div className="flex items-start">
              <Mail className="h-6 w-6 text-red-600 mr-4 mt-1" />
              <div>
                <h4 className="font-semibold text-gray-900">Email</h4>
                <p className="text-gray-600">hola@cynicalgirl.com</p>
              </div>
            </div>
            
            <div className="flex items-start">
              <MapPin className="h-6 w-6 text-red-600 mr-4 mt-1" />
              <div>
                <h4 className="font-semibold text-gray-900">Ubicación</h4>
                <p className="text-gray-600">Ciudad de Panamá, Panamá</p>
              </div>
            </div>
            
            <div className="flex items-start">
              <div className="w-6 h-6 bg-red-600 rounded-full flex items-center justify-center mr-4 mt-1">
                <Instagram className="h-4 w-4 text-white" />
              </div>
              <div>
                <h4 className="font-semibold text-gray-900">Redes Sociales</h4>
                <div className="flex space-x-4 mt-2">
                  {socialMedia.map((social) => (
                    <a
                      key={social.platform}
                      href={social.url}
                      className="text-gray-600 hover:text-red-600 transition-colors"
                    >
                      <social.icon className="h-5 w-5" />
                    </a>
                  ))}
                </div>
              </div>
            </div>
          </div>
          
          <div className="mt-8 bg-gray-50 p-6 rounded-lg">
            <h4 className="font-semibold text-gray-900 mb-4">Horario de Atención</h4>
            <p className="text-gray-600">Lunes a Viernes: 9:00 AM - 6:00 PM</p>
            <p className="text-gray-600">Sábados: 10:00 AM - 2:00 PM</p>
          </div>
        </div>
      </div>
    </section>
  );
}

