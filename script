import React, { useState, useEffect } from 'react';
import { Camera, FileText, Flashlight, Plus, Compass, Clock, Download, Music, Radio, PhoneCall, Video, Activity, 
  Ruler, SpeedDial, Mountain, Wifi, Battery, Calculator, Calendar, Map, ThermometerSun, Umbrella, Moon, 
  BarChart3, QrCode, Timer } from 'lucide-react';
import { Card, CardContent } from '@/components/ui/card';
import { Alert, AlertDescription } from '@/components/ui/alert';

const ToolSection = ({ title, tools }) => (
  <div className="mb-8">
    <h2 className="text-xl font-bold mb-4 px-4">{title}</h2>
    <div className="grid grid-cols-4 gap-4 px-4">
      {tools.map((tool) => (
        <Card 
          key={tool.name} 
          className="flex flex-col items-center p-4 cursor-pointer hover:bg-gray-100 transition-colors"
          onClick={tool.action}
        >
          <div className={`p-3 rounded-lg mb-2 ${tool.bgColor}`}>
            {tool.icon}
          </div>
          <span className="text-sm text-center">{tool.name}</span>
        </Card>
      ))}
    </div>
  </div>
);

const App = () => {
  const [flashlightOn, setFlashlightOn] = useState(false);
  const [selectedTool, setSelectedTool] = useState(null);
  const [batteryLevel, setBatteryLevel] = useState(100);
  const [wifiStrength, setWifiStrength] = useState(0);
  const [location, setLocation] = useState(null);
  const [weather, setWeather] = useState(null);
  const [qrResult, setQrResult] = useState(null);
  const [showAlert, setShowAlert] = useState(false);

  // Simulation de la récupération des données du système
  useEffect(() => {
    // Simulation batterie
    const batteryInterval = setInterval(() => {
      setBatteryLevel(prev => Math.max(0, prev - 0.1));
    }, 60000);

    // Simulation force WiFi
    const wifiInterval = setInterval(() => {
      setWifiStrength(Math.floor(Math.random() * 5));
    }, 10000);

    // Simulation GPS
    if (navigator.geolocation) {
      navigator.geolocation.watchPosition(
        (position) => {
          setLocation({
            lat: position.coords.latitude,
            lng: position.coords.longitude
          });
        },
        null,
        { enableHighAccuracy: true }
      );
    }

    return () => {
      clearInterval(batteryInterval);
      clearInterval(wifiInterval);
    };
  }, []);

  const basicTools = [
    {
      name: "Torche",
      icon: <Flashlight size={24} color={flashlightOn ? "#fbbf24" : "#000"} />,
      action: () => {
        setFlashlightOn(!flashlightOn);
        setShowAlert(true);
      },
      bgColor: "bg-orange-400"
    },
    {
      name: "Caméra QR",
      icon: <QrCode size={24} />,
      action: () => {
        setSelectedTool("qrscanner");
        // Simulation scan QR
        setTimeout(() => {
          setQrResult("https://example.com");
          setShowAlert(true);
        }, 2000);
      },
      bgColor: "bg-purple-400"
    },
    {
      name: "Notes",
      icon: <FileText size={24} />,
      action: () => setSelectedTool("notes"),
      bgColor: "bg-yellow-400"
    },
    {
      name: "Calculatrice",
      icon: <Calculator size={24} />,
      action: () => setSelectedTool("calculator"),
      bgColor: "bg-blue-400"
    }
  ];

  const systemTools = [
    {
      name: "WiFi Scanner",
      icon: <Wifi size={24} />,
      action: () => {
        setSelectedTool("wifiscan");
        setShowAlert(true);
      },
      bgColor: "bg-blue-500"
    },
    {
      name: "Batterie",
      icon: <Battery size={24} />,
      action: () => setSelectedTool("battery"),
      bgColor: "bg-green-500"
    },
    {
      name: "Horloge",
      icon: <Clock size={24} />,
      action: () => setSelectedTool("clock"),
      bgColor: "bg-gray-500"
    },
    {
      name: "Calendrier",
      icon: <Calendar size={24} />,
      action: () => setSelectedTool("calendar"),
      bgColor: "bg-red-500"
    }
  ];

  const environmentTools = [
    {
      name: "Météo",
      icon: <ThermometerSun size={24} />,
      action: () => setSelectedTool("weather"),
      bgColor: "bg-yellow-500"
    },
    {
      name: "Boussole GPS",
      icon: <Compass size={24} />,
      action: () => {
        setSelectedTool("compass");
        if (location) setShowAlert(true);
      },
      bgColor: "bg-blue-600"
    },
    {
      name: "Phase Lunaire",
      icon: <Moon size={24} />,
      action: () => setSelectedTool("moon"),
      bgColor: "bg-purple-600"
    },
    {
      name: "Baromètre",
      icon: <Umbrella size={24} />,
      action: () => setSelectedTool("barometer"),
      bgColor: "bg-teal-600"
    }
  ];

  const measurementTools = [
    {
      name: "Chronomètre",
      icon: <Timer size={24} />,
      action: () => setSelectedTool("timer"),
      bgColor: "bg-red-600"
    },
    {
      name: "Niveau",
      icon: <Ruler size={24} />,
      action: () => setSelectedTool("level"),
      bgColor: "bg-green-600"
    },
    {
      name: "Décibels",
      icon: <BarChart3 size={24} />,
      action: () => setSelectedTool("decibels"),
      bgColor: "bg-yellow-600"
    },
    {
      name: "GPS Altitude",
      icon: <Mountain size={24} />,
      action: () => setSelectedTool("altitude"),
      bgColor: "bg-blue-600"
    }
  ];

  const getAlertMessage = () => {
    switch (selectedTool) {
      case "wifiscan":
        return `Force du signal WiFi: ${wifiStrength}/4`;
      case "compass":
        return `Position: ${location?.lat.toFixed(4)}, ${location?.lng.toFixed(4)}`;
      case "qrscanner":
        return `QR Code détecté: ${qrResult}`;
      default:
        return flashlightOn ? "Torche activée" : "Torche désactivée";
    }
  };

  return (
    <div className="min-h-screen bg-gray-50">
      <header className="bg-pink-600 text-white p-4 flex items-center justify-between">
        <div className="flex items-center">
          <h1 className="text-xl font-bold">Super Outils</h1>
        </div>
        <div className="flex items-center space-x-4">
          <span>{batteryLevel.toFixed(0)}%</span>
          <Wifi size={24} />
        </div>
      </header>

      <main className="py-6">
        {showAlert && (
          <Alert className="mx-4 mb-6">
            <AlertDescription>
              {getAlertMessage()}
            </AlertDescription>
          </Alert>
        )}
        
        <ToolSection title="Outils Essentiels" tools={basicTools} />
        <ToolSection title="Outils Système" tools={systemTools} />
        <ToolSection title="Environnement" tools={environmentTools} />
        <ToolSection title="Mesures" tools={measurementTools} />
      </main>
    </div>
  );
};

export default App;
