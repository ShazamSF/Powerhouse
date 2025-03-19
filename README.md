import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { ShoppingCart } from "lucide-react";

const products = [
  { id: 1, name: "Whey Protein", price: 49.99, image: "/images/whey-protein.jpg" },
  { id: 2, name: "Creatine Monohydrate", price: 29.99, image: "/images/creatine.jpg" },
  { id: 3, name: "Pre-Workout Booster", price: 39.99, image: "/images/preworkout.jpg" },
  { id: 4, name: "BCAA Recovery", price: 24.99, image: "/images/bcaa.jpg" },
];

export default function PowerhouseHulk() {
  const [cart, setCart] = useState([]);

  const addToCart = (product) => {
    setCart([...cart, product]);
    trackEvent("add_to_cart", { product_id: product.id, name: product.name, price: product.price });
  };

  const trackEvent = (eventName, data) => {
    console.log("Tracking Event:", eventName, data);
    // Send event data to WebSDK Data Cloud API here
  };

  return (
    <div className="p-6">
      <h1 className="text-3xl font-bold mb-4">Powerhouse Hulk - Gym Essentials</h1>
      <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
        {products.map((product) => (
          <Card key={product.id} className="p-4 text-center">
            <img src={product.image} alt={product.name} className="h-40 w-full object-cover mb-2" />
            <CardContent>
              <h2 className="text-lg font-semibold">{product.name}</h2>
              <p className="text-gray-600">${product.price}</p>
              <Button className="mt-2" onClick={() => addToCart(product)}>
                <ShoppingCart className="mr-2 h-5 w-5" /> Add to Cart
              </Button>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
