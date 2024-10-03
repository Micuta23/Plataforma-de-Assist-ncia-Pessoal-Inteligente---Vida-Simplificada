import React from 'react';
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { CalendarDays, DollarSign, Heart, Leaf, FileText } from 'lucide-react';

const Index = () => {
  return (
    <div className="min-h-screen bg-gray-100 p-8">
      <h1 className="text-4xl font-bold mb-8 text-center">Vida+ Simplificada</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <FeatureCard
          icon={<CalendarDays className="h-8 w-8 text-blue-500" />}
          title="Organização de Tarefas"
          description="Gerencie suas tarefas e rotinas com IA adaptativa."
        />
        <FeatureCard
          icon={<DollarSign className="h-8 w-8 text-green-500" />}
          title="Gestão Financeira"
          description="Acompanhe gastos e receba insights financeiros personalizados."
        />
        <FeatureCard
          icon={<Heart className="h-8 w-8 text-red-500" />}
          title="Bem-Estar e Saúde"
          description="Monitore sua saúde e receba recomendações personalizadas."
        />
        <FeatureCard
          icon={<Leaf className="h-8 w-8 text-green-600" />}
          title="Consumo Consciente"
          description="Faça escolhas sustentáveis e reduza seu impacto ambiental."
        />
        <FeatureCard
          icon={<FileText className="h-8 w-8 text-purple-500" />}
          title="Gestão de Documentos"
          description="Organize e acesse seus documentos importantes facilmente."
        />
      </div>
    </div>
  );
};

const FeatureCard = ({ icon, title, description }) => {
  return (
    <Card>
      <CardHeader className="flex flex-row items-center space-x-4">
        {icon}
        <CardTitle>{title}</CardTitle>
      </CardHeader>
      <CardContent>
        <p>{description}</p>
      </CardContent>
    </Card>
  );
};

export default Index;

Agora, vamos criar um componente de layout para nossa aplicação:


src/components/Layout.jsx
import React from 'react';
import { Link } from 'react-router-dom';
import { CalendarDays, DollarSign, Heart, Leaf, FileText, Home } from 'lucide-react';

const Layout = ({ children }) => {
  return (
    <div className="flex h-screen bg-gray-100">
      <nav className="w-64 bg-white shadow-lg">
        <div className="p-4">
          <h1 className="text-2xl font-bold">Vida+ Simplificada</h1>
        </div>
        <ul className="space-y-2 p-4">
          <NavItem to="/" icon={<Home />} text="Início" />
          <NavItem to="/tarefas" icon={<CalendarDays />} text="Tarefas" />
          <NavItem to="/financas" icon={<DollarSign />} text="Finanças" />
          <NavItem to="/saude" icon={<Heart />} text="Saúde" />
          <NavItem to="/sustentabilidade" icon={<Leaf />} text="Sustentabilidade" />
          <NavItem to="/documentos" icon={<FileText />} text="Documentos" />
        </ul>
      </nav>
      <main className="flex-1 overflow-y-auto p-8">
        {children}
      </main>
    </div>
  );
};

const NavItem = ({ to, icon, text }) => {
  return (
    <li>
      <Link to={to} className="flex items-center space-x-2 p-2 hover:bg-gray-200 rounded">
        {icon}
        <span>{text}</span>
      </Link>
    </li>
  );
};

export default Layout;

Agora, vamos atualizar o arquivo `App.jsx` para usar o novo componente de Layout:


src/App.jsx
import { Toaster } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { navItems } from "./nav-items";
import Layout from "./components/Layout";

const queryClient = new QueryClient();

const App = () => (
  <QueryClientProvider client={queryClient}>
    <TooltipProvider>
      <Toaster />
      <BrowserRouter>
        <Layout>
          <Routes>
            {navItems.map(({ to, page }) => (
              <Route key={to} path={to} element={page} />
            ))}
          </Routes>
        </Layout>
      </BrowserRouter>
    </TooltipProvider>
  </QueryClientProvider>
);

export default App;

Por fim, vamos atualizar o arquivo `nav-items.jsx` para incluir as novas rotas:


src/nav-items.jsx
import { HomeIcon, CalendarDays, DollarSign, Heart, Leaf, FileText } from "lucide-react";
import Index from "./pages/Index.jsx";

export const navItems = [
  {
    title: "Início",
    to: "/",
    icon: <HomeIcon className="h-4 w-4" />,
    page: <Index />,
  },
  {
    title: "Tarefas",
    to: "/tarefas",
    icon: <CalendarDays className="h-4 w-4" />,
    page: <div>Página de Tarefas</div>,
  },
  {
    title: "Finanças",
    to: "/financas",
    icon: <DollarSign className="h-4 w-4" />,
    page: <div>Página de Finanças</div>,
  },
  {
    title: "Saúde",
    to: "/saude",
    icon: <Heart className="h-4 w-4" />,
    page: <div>Página de Saúde</div>,
  },
  {
    title: "Sustentabilidade",
    to: "/sustentabilidade",
    icon: <Leaf className="h-4 w-4" />,
    page: <div>Página de Sustentabilidade</div>,
  },
  {
    title: "Documentos",
    to: "/documentos",
    icon: <FileText className="h-4 w-4" />,
    page: <div>Página de Documentos</div>,
  },
];
