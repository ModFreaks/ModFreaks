import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { useEffect } from "react";

const products = [
  {
    name: "LED Underglow Lights",
    price: "$25",
    description: "Lights up under the car and on the ground. Futuristic vibes guaranteed.",
  },
  {
    name: "LED Grid Police Lights",
    price: "$20",
    description: "Glows red and blue on the front grills. Authority mode: ON.",
  },
  {
    name: "Car Logo Door Light",
    price: "$8",
    description: "Projects your car's logo on the ground when you open the door. Clean and classy.",
  },
];

export default function ModFreaksPage() {
  useEffect(() => {
    const clickSound = new Audio("/click.mp3");
    const hoverSound = new Audio("/hover.mp3");

    const buttons = document.querySelectorAll("button");
    buttons.forEach((btn) => {
      btn.addEventListener("click", () => clickSound.play());
      btn.addEventListener("mouseenter", () => hoverSound.play());
    });

    return () => {
      buttons.forEach((btn) => {
        btn.removeEventListener("click", () => clickSound.play());
        btn.removeEventListener("mouseenter", () => hoverSound.play());
      });
    };
  }, []);

  return (
    <div className="min-h-screen bg-gradient-to-b from-black via-[#0f0f0f] to-black text-white px-4 py-10 space-y-10 font-sans overflow-hidden relative">
      <motion.div
        animate={{ rotate: 360 }}
        transition={{ repeat: Infinity, duration: 60, ease: "linear" }}
        className="absolute w-[300px] h-[300px] bg-[#00FFD1]/10 rounded-full blur-3xl top-[-100px] left-[-100px]"
      />

      <motion.h1
        initial={{ opacity: 0, y: -50 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 1 }}
        className="text-4xl md:text-6xl font-bold text-center text-[#00FFD1] drop-shadow-lg"
      >
        ModFreaks
      </motion.h1>

      <motion.p
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ delay: 0.5, duration: 1 }}
        className="text-center text-lg md:text-xl max-w-2xl mx-auto text-gray-300"
      >
        Elevate your car game. Drive like a freak. Mod like a boss.
      </motion.p>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-6xl mx-auto z-10">
        {products.map((product, i) => (
          <motion.div
            key={i}
            initial={{ opacity: 0, scale: 0.9 }}
            whileInView={{ opacity: 1, scale: 1 }}
            transition={{ duration: 0.5, delay: i * 0.2 }}
          >
            <Card className="bg-[#111] border border-[#00FFD1] rounded-2xl shadow-xl hover:scale-105 transition-transform">
              <CardContent className="p-6 space-y-4">
                <h3 className="text-xl font-semibold text-[#00FFD1]">{product.name}</h3>
                <p className="text-gray-400">{product.description}</p>
                <p className="text-lg font-bold text-white">{product.price}</p>
                <Button variant="outline" className="border-[#00FFD1] text-[#00FFD1] w-full">DM to Order</Button>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>

      <motion.footer
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ delay: 1 }}
        className="text-center text-gray-600 text-sm pt-10"
      >
        Website by ModFreaks. Contact info will be added shortly.
      </motion.footer>
    </div>
  );
}
