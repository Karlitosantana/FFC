import React, { useState, useEffect, useRef } from 'react';
import { Card, CardContent } from '@/components/ui/card';
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs';
import { Input } from '@/components/ui/input';
import { Button } from '@/components/ui/button';
import { Checkbox } from '@/components/ui/checkbox';
import { Label } from '@/components/ui/label';
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select';
import { Search, ShoppingCart, Plus, Minus, X, Filter, Download, Save, FileText, Printer } from 'lucide-react';
import _ from 'lodash';

const CateringConfigurator = () => {
  // State management
  const [activeCategory, setActiveCategory] = useState('chlebicky');
  const [searchQuery, setSearchQuery] = useState('');
  const [cart, setCart] = useState([]);
  const [showCart, setShowCart] = useState(false);
  const [showContactForm, setShowContactForm] = useState(false);
  const [filters, setFilters] = useState({
    vegetarian: false,
    vegan: false,
    glutenFree: false,
    priceRange: [0, 2000],
    maxPrice: 2000,
  });
  const [contactInfo, setContactInfo] = useState({
    name: '',
    email: '',
    phone: '',
    eventDate: '',
    eventTime: '',
    guests: '',
    eventType: '',
    specialRequirements: ''
  });

  // Categories for navigation
  const categories = [
    { id: 'all', name: 'Vše', icon: '🍽️' },
    { id: 'chlebicky', name: 'Chlebíčky & Kanapky', icon: '🥪' },
    { id: 'oblozene-misy', name: 'Obložené mísy', icon: '🧀' },
    { id: 'finger-food', name: 'Finger Food', icon: '👌' },
    { id: 'zmrzlinovy-bar', name: 'Zmrzlinový bar', icon: '🍦' },
    { id: 'lehke-obcerstveni', name: 'Lehké občerstvení', icon: '🥗' },
    { id: 'salaty', name: 'Saláty', icon: '🥬' },
    { id: 'pomazanky', name: 'Pomazánky', icon: '🧈' },
    { id: 'quiche', name: 'Quiche', icon: '🥧' },
    { id: 'sendvice', name: 'Sendviče', icon: '🥖' },
    { id: 'teply-bufet', name: 'Teplý bufet', icon: '🍲' },
    { id: 'studeny-bufet', name: 'Studený bufet', icon: '🍱' },
    { id: 'dezerty', name: 'Dezerty & Ovoce', icon: '🍰' },
    { id: 'korytka', name: 'Korýtka', icon: '🍽️' },
    { id: 'grilovani', name: 'Grilovací nabídka', icon: '🔥' },
    { id: 'rauty', name: 'Rautové bufety', icon: '🍴' },
    { id: 'polévky', name: 'Polévky', icon: '🍜' },
    { id: 'sluzby', name: 'Služby & Inventář', icon: '🛠️' }
  ];

  // Catalog data from PDFs
  const catalogData = {
    'chlebicky': [
      { id: 'ch1', name: 'Šunkový', price: 35, amount: '1 ks', description: 'Chlebíček se šunkou', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch2', name: 'Sýrový', price: 35, amount: '1 ks', description: 'Chlebíček se sýrem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch3', name: 'Šunkový s vejcem', price: 35, amount: '1 ks', description: 'Chlebíček se šunkou a vejcem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch4', name: 'Labužnický', price: 35, amount: '1 ks', description: 'Labužnický chlebíček', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch5', name: 'Herkules', price: 35, amount: '1 ks', description: 'Chlebíček Herkules', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch6', name: 'S tuňákem a vejcem', price: 40, amount: '1 ks', description: 'Chlebíček s tuňákem a vejcem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch7', name: 'S uzeným lososem', price: 45, amount: '1 ks', description: 'Chlebíček s uzeným lososem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ch8', name: 'Rajčatový s bazalkou', price: 35, amount: '1 ks', description: 'Chlebíček rajčatový s bazalkou', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Chlebíčky', minOrder: 10 },
      { id: 'ka1', name: 'Sýrové s okurkou', price: 32, amount: '1 ks', description: 'Kanapka sýrová s okurkou', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka2', name: 'Uzeninové', price: 32, amount: '1 ks', description: 'Kanapka uzeninová', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka3', name: 'Lahůdkové', price: 32, amount: '1 ks', description: 'Kanapka lahůdková', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka4', name: 'Tuňákové', price: 32, amount: '1 ks', description: 'Kanapka tuňáková', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka5', name: 'S Camembertem', price: 32, amount: '1 ks', description: 'Kanapka s Camembertem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka6', name: 'Vaječné', price: 32, amount: '1 ks', description: 'Kanapka vaječná', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka7', name: 'Křenové s uzeninou', price: 32, amount: '1 ks', description: 'Kanapka křenová s uzeninou', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka8', name: 'S uzeným lososem', price: 39, amount: '1 ks', description: 'Kanapka s uzeným lososem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'ka9', name: 'Kaviárové vejce', price: 39, amount: '1 ks', description: 'Kanapka kaviárové vejce', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Kanapky', minOrder: 10 },
      { id: 'vip1', name: 'Se schwarzwaldskou šunkou, mozzarellou, cherry rajčátky a balsamicem - guacamole', price: 75, amount: '1 ks', description: 'VIP chlebíček se schwarzwaldskou šunkou', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'VIP Chlebíčky', minOrder: 10 },
      { id: 'vip2', name: 'S čerstvým sýrem, ostružinami, šalotkou a tymiánem – humus s červenou řepou', price: 75, amount: '1 ks', description: 'VIP chlebíček s čerstvým sýrem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'VIP Chlebíčky', minOrder: 10 },
      { id: 'vip3', name: 'S kozím sýrem, granátovým jablkem, sultánkami a vl.ořechem - guacamole', price: 75, amount: '1 ks', description: 'VIP chlebíček s kozím sýrem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'VIP Chlebíčky', minOrder: 10 },
      { id: 'jhu1', name: 'Jednohubky - mix', price: 18, amount: '1 ks', description: 'Variace jednohubek, minimální odběr 20 ks', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Jednohubky', minOrder: 20 },
    ],
    'oblozene-misy': [
      { id: 'om1', name: 'Uzeninová česká', price: 720, amount: '1 kg', description: 'Česká uzeninová mísa', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om2', name: 'Sýrová česká', price: 720, amount: '1 kg', description: 'Česká sýrová mísa', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om3', name: 'Míchaná česká', price: 720, amount: '1 kg', description: 'Mísa s českými uzeninami a sýry', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om4', name: 'Uzeninová zahraniční', price: 1150, amount: '1 kg', description: 'Zahraniční uzeninová mísa', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om5', name: 'Sýrová zahraniční', price: 1150, amount: '1 kg', description: 'Zahraniční sýrová mísa', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om6', name: 'Míchaná zahraniční', price: 1150, amount: '1 kg', description: 'Mísa se zahraničními uzeninami a sýry', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om7', name: 'Zabijačkový mix', price: 720, amount: '1 kg', description: 'Mix zabijačkových specialit', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om8', name: 'Uzený mix', price: 650, amount: '1 kg', description: 'Mix uzených specialit', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om9', name: 'Kuřecí mini řízečky', price: 650, amount: '1 kg', description: 'Mísa s kuřecími mini řízečky', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om10', name: 'Vepřové mini řízečky', price: 650, amount: '1 kg', description: 'Mísa s vepřovými mini řízečky', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om11', name: 'Zeleninová', price: 355, amount: '1 kg', description: 'Zeleninová mísa', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om12', name: 'Španělský tapas', price: 1399, amount: '1 kg', description: 'Španělský tapas', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om13', name: 'Řecký tapas', price: 1399, amount: '1 kg', description: 'Řecký tapas', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om14', name: 'Ovocná mísa', price: 330, amount: '1 kg', description: 'Ovocná mísa', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
      { id: 'om15', name: 'Ovocný salát', price: 450, amount: '1 kg', description: 'Ovocný salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Obložené mísy', minOrder: 1 },
    ],
    'finger-food': [
      { id: 'ff1', name: 'Špíz Caprese', price: 38, amount: '1 ks', description: 'Cherry raj., mozzarella, bazalka', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff2', name: 'Filírovaná panenka v pepři', price: 55, amount: '1 ks', description: 'Křenová pěna, grissini, výhonky', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Finger Food', minOrder: 1 },
      { id: 'ff3', name: 'Domácí masové páté', price: 42, amount: '1 ks', description: 'Kyselá okurka, křupavá cibulka, pečivo', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Finger Food', minOrder: 1 },
      { id: 'ff4', name: 'Nakládaná Feta', price: 45, amount: '1 ks', description: 'V černém sezamu, sušená rajčata', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff5', name: 'Uzený losos', price: 60, amount: '1 ks', description: 'S variací oliv, citrus', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff6', name: 'Trhaná vepřové v BBQ', price: 42, amount: '1 ks', description: 'Bruschetta, výhonky', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Finger Food', minOrder: 1 },
      { id: 'ff7', name: 'Mini páreček v listovém těstě', price: 38, amount: '1 ks', description: 'Rajčatové sugo', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Finger Food', minOrder: 1 },
      { id: 'ff8', name: 'Měšec ze šunky od kosti', price: 38, amount: '1 ks', description: 'S křenovým relishem, výhonky', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff9', name: 'Smažená mozzarella', price: 55, amount: '1 ks', description: 'Chorizo, oliva', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Finger Food', minOrder: 1 },
      { id: 'ff10', name: 'Šopský salát', price: 40, amount: '1 ks', description: 'S balkánským sýrem', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff11', name: 'Marinovaná červená řepa', price: 42, amount: '1 ks', description: 'S kozím sýrem, výhonky', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff12', name: 'Pěna z červené řepy', price: 40, amount: '1 ks', description: 'Chlebový chips, výhonky', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Finger Food', minOrder: 1 },
      { id: 'ff13', name: 'Šlehaná bylinková pěna', price: 40, amount: '1 ks', description: 'S křupavou zeleninou', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff14', name: 'Domácí Nachos', price: 38, amount: '1 ks', description: 'S rajčatovou salsou', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
      { id: 'ff15', name: 'Grilovaná krevetka', price: 65, amount: '1 ks', description: 'Salátová okurka, avokádové páté', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Finger Food', minOrder: 1 },
    ],
    'zmrzlinovy-bar': [
      { id: 'zb1', name: 'Zapůjčení zmrzlinového baru', price: 800, amount: '1 ks', description: 'Chladící prosklená vitrína o obsahu 2x 5l zmrzliny nebo 4x 2,5l zmrzliny, Nabírací kleště na zmrzlinu', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb2', name: 'Zmrzlina ve vaničce dle výběru', price: 850, amount: '5 l', description: 'Zmrzlina ve vaničce dle výběru', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb3', name: 'Zmrzlina ve vaničce dle výběru', price: 450, amount: '2,5 l', description: 'Zmrzlina ve vaničce dle výběru', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb4', name: 'Posyp zdobení – 2 druhy', price: 150, amount: '100 g', description: 'Posyp zdobení – 2 druhy', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb5', name: 'Posyp zdobení – 4 druhy', price: 250, amount: '200 g', description: 'Posyp zdobení – 4 druhy', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb6', name: 'Koktejlové ovoce', price: 150, amount: '240 g', description: 'Koktejlové ovoce', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb7', name: 'Oplatky, trubičky', price: 120, amount: '100 g', description: 'Oplatky, trubičky', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb8', name: 'Karamelové sušenky', price: 100, amount: '100 g', description: 'Karamelové sušenky', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb9', name: 'Topping (jahoda, čokoláda, karamel)', price: 110, amount: '200 g', description: 'Topping (jahoda, čokoláda, karamel)', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb10', name: 'Želé bonbóny', price: 100, amount: '100 g', description: 'Želé bonbóny', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb11', name: 'Lentilky', price: 100, amount: '100 g', description: 'Lentilky', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb12', name: 'Šlehačka ve spreji', price: 200, amount: '0,5 l', description: 'Šlehačka ve spreji', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb13', name: 'Šlehačka ve spreji', price: 110, amount: '250 ml', description: 'Šlehačka ve spreji', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb14', name: 'Zmrzlinový kornout', price: 50, amount: '10 ks', description: 'Zmrzlinový kornout', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Zmrzlinový bar', minOrder: 1 },
      { id: 'zb15', name: 'Zapůjčení porcelánové misky + lžička', price: 10, amount: '1 ks', description: 'Zapůjčení porcelánové misky + lžička', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Zmrzlinový bar', minOrder: 1 },
    ],
    // Add categories for all the menu sections
    'salaty': [
      { id: 'sa1', name: 'Míchaný zeleninový salát', price: 27, amount: 'porce', description: 'Míchaný zeleninový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'sa2', name: 'Zel. salát s modrým sýrem', price: 30, amount: 'porce', description: 'Zeleninový salát s modrým sýrem', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'sa3', name: 'Pestrý listový salát', price: 27, amount: 'porce', description: 'Pestrý listový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'sa4', name: 'Šopský salát', price: 30, amount: 'porce', description: 'Šopský salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'sa5', name: 'Salát z červené čočky', price: 29, amount: 'porce', description: 'Salát z červené čočky', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'sa6', name: 'Sal. z čer. řepy a kozí sýr', price: 40, amount: 'porce', description: 'Salát z červené řepy a kozí sýr', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'sa7', name: 'Salát Coleslaw', price: 25, amount: 'porce', description: 'Salát Coleslaw', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      // Additional salads from other sections
      { id: 'sa8', name: 'Bramborový salát - klasický', price: 295, amount: '1 kg', description: 'Klasický bramborový salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Bramborové saláty', minOrder: 1 },
      { id: 'sa9', name: 'Bramborový salát - Vídeňský', price: 295, amount: '1 kg', description: 'Vídeňský bramborový salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Bramborové saláty', minOrder: 1 },
      { id: 'sa10', name: 'Bramborový salát - Břeclavský', price: 295, amount: '1 kg', description: 'Břeclavský bramborový salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Bramborové saláty', minOrder: 1 },
      { id: 'sa11', name: 'Bramborový salát - Francouzský', price: 295, amount: '1 kg', description: 'Francouzský bramborový salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Bramborové saláty', minOrder: 1 },
      { id: 'sa12', name: 'Coleslaw', price: 305, amount: '1 kg', description: 'Salát Coleslaw', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 1 },
      { id: 'sa13', name: 'Luštěninový salát - čočkový', price: 360, amount: '1 kg', description: 'Čočkový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Luštěninové saláty', minOrder: 1 },
      { id: 'sa14', name: 'Luštěninový salát - fazolový', price: 360, amount: '1 kg', description: 'Fazolový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Luštěninové saláty', minOrder: 1 },
      { id: 'sa15', name: 'Luštěninový salát - cizrnový', price: 360, amount: '1 kg', description: 'Cizrnový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Luštěninové saláty', minOrder: 1 },
    ],
    // Additional categories following the same pattern
    'pomazanky': [
      { id: 'po1', name: 'Vaječná', price: 49, amount: '100 g', description: 'Vaječná pomazánka', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po2', name: 'Šunková pěna', price: 49, amount: '100 g', description: 'Šunková pěna', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po3', name: 'Bylinková s tvarohem', price: 49, amount: '100 g', description: 'Bylinková pomazánka s tvarohem', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po4', name: 'Škvarková', price: 49, amount: '100 g', description: 'Škvarková pomazánka', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po5', name: 'Tuňáková', price: 55, amount: '100 g', description: 'Tuňáková pomazánka', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po6', name: 'Guacamole', price: 65, amount: '100 g', description: 'Guacamole', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po7', name: 'Hummus', price: 55, amount: '100 g', description: 'Hummus', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po8', name: 'Hummus s červenou řepou', price: 55, amount: '100 g', description: 'Hummus s červenou řepou', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po9', name: 'Hummus s olivami', price: 55, amount: '100 g', description: 'Hummus s olivami', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
      { id: 'po10', name: 'Hummus kořeněný', price: 55, amount: '100 g', description: 'Kořeněný hummus', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Pomazánky', minOrder: 300 },
    ],
    'quiche': [
      { id: 'qu1', name: 'Se šunkou a ementálem', price: 425, amount: '1 ks', description: 'Quiche se šunkou a ementálem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Quiche - Slaný koláč', minOrder: 1 },
      { id: 'qu2', name: 'S angl. slaninou a cibulí', price: 425, amount: '1 ks', description: 'Quiche s anglickou slaninou a cibulí', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Quiche - Slaný koláč', minOrder: 1 },
      { id: 'qu3', name: 'S uzeným lososem a koprem', price: 520, amount: '1 ks', description: 'Quiche s uzeným lososem a koprem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Quiche - Slaný koláč', minOrder: 1 },
      { id: 'qu4', name: 'Se špenátem a Camembertem', price: 425, amount: '1 ks', description: 'Quiche se špenátem a Camembertem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Quiche - Slaný koláč', minOrder: 1 },
      { id: 'qu5', name: 'Zeleninový', price: 425, amount: '1 ks', description: 'Zeleninový quiche', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Quiche - Slaný koláč', minOrder: 1 },
    ],
    'sendvice': [
      { id: 'se1', name: 'BLT', price: 85, amount: '1 ks', description: 'Toast, majonéza, slanina, rajče, salát', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Sendviče', minOrder: 10 },
      { id: 'se2', name: 'Club sendvič', price: 105, amount: '1 ks', description: 'Toast, majonéza, kuřecí prso, vaječná omeleta, salát, rajče', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Sendviče', minOrder: 10 },
      { id: 'se3', name: 'Francouzský sendvič', price: 89, amount: '1 ks', description: 'Toast, máslo, šunka od kosti, ementál, salát, okurka', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Sendviče', minOrder: 10 },
    ],
    'lehke-obcerstveni': [
      // This section combines various light refreshments
      { id: 'lo1', name: 'Jednohubky', price: 18, amount: '1 ks', description: 'Nabízíme také celou škálu jednohubek za jednotnou cenu', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Jednohubky', minOrder: 20 },
      { id: 'lo2', name: 'BLT sendvič', price: 85, amount: '1 ks', description: 'Toast, majonéza, slanina, rajče, salát', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Sendviče', minOrder: 10 },
      { id: 'lo3', name: 'Club sendvič', price: 105, amount: '1 ks', description: 'Toast, majonéza, kuřecí prso, vaječná omeleta, salát, rajče', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Sendviče', minOrder: 10 },
      { id: 'lo4', name: 'Francouzský sendvič', price: 89, amount: '1 ks', description: 'Toast, máslo, šunka od kosti, ementál, salát, okurka', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Sendviče', minOrder: 10 },
      { id: 'lo5', name: 'Míchaný zeleninový salát', price: 27, amount: 'porce', description: 'Míchaný zeleninový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'lo6', name: 'Zel. salát s modrým sýrem', price: 30, amount: 'porce', description: 'Zeleninový salát s modrým sýrem', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'lo7', name: 'Pestrý listový salát', price: 27, amount: 'porce', description: 'Pestrý listový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'lo8', name: 'Šopský salát', price: 30, amount: 'porce', description: 'Šopský salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'lo9', name: 'Salát z červené čočky', price: 29, amount: 'porce', description: 'Salát z červené čočky', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'lo10', name: 'Sal. z čer. řepy a kozí sýr', price: 40, amount: 'porce', description: 'Salát z červené řepy a kozí sýr', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
      { id: 'lo11', name: 'Salát Coleslaw', price: 25, amount: 'porce', description: 'Salát Coleslaw', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Saláty', minOrder: 10 },
    ],
    // Continue with more categories
    'grilovani': [
      { id: 'gr1', name: 'Zapůjčení grilu', price: 800, amount: '1 ks', description: 'Zapůjčení grilu', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Grilovací nabídka', minOrder: 1 },
      { id: 'gr2', name: 'Propan do 30 osob', price: 250, amount: '1 ks', description: 'Propan do 30 osob', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Grilovací nabídka', minOrder: 1 },
      { id: 'gr3', name: 'Propan nad 30 osob', price: 350, amount: '1 ks', description: 'Propan nad 30 osob', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Grilovací nabídka', minOrder: 1 },
      { id: 'gr4', name: 'Zapůjčení rožně do 25kg včetně paliva a vyčištění', price: 1700, amount: '1 ks', description: 'Zapůjčení rožně do 25kg včetně paliva a vyčištění', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Grilovací nabídka', minOrder: 1 },
      { id: 'gr5', name: 'Naložené předpečené sele', price: 435, amount: '1 kg', description: 'Naložené předpečené sele', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Jídla na rožeň', minOrder: 1 },
      { id: 'gr6', name: 'Naložená předpečená vepřová kýta s.k.', price: 465, amount: '1 kg', description: 'Naložená předpečená vepřová kýta s.k.', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Jídla na rožeň', minOrder: 1 },
      // Vegetariánské
      { id: 'gr7', name: 'Grilovaný slovenský oštěpek se švestkovou omáčkou', price: 95, amount: '1 ks', description: 'Grilovaný slovenský oštěpek se švestkovou omáčkou', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské', minOrder: 1 },
      { id: 'gr8', name: 'Grilovaný sýr Halloumi', price: 105, amount: '100 g', description: 'Grilovaný sýr Halloumi', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské', minOrder: 1 },
      { id: 'gr9', name: 'Grilovaný naložený hermelín s brusinkami', price: 95, amount: '100 g', description: 'Grilovaný naložený hermelín s brusinkami', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské', minOrder: 1 },
      { id: 'gr10', name: 'Grilovaná zelenina', price: 355, amount: '1 kg', description: 'Cuketa, paprika, cibule, cherry rajče, žampion', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské', minOrder: 1 },
      { id: 'gr11', name: 'Kukuřičný klas', price: 355, amount: '1 kg', description: 'Kukuřičný klas', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské', minOrder: 1 },
      // Mini burgery a hot dogy
      { id: 'gr12', name: 'Mini hamburger hovězí', price: 105, amount: '1 ks', description: 'Mini hamburger hovězí', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mini burgery a hot dogy', minOrder: 10 },
      { id: 'gr13', name: 'Mini hamburger s trhaným masem', price: 105, amount: '1 ks', description: 'Mini hamburger s trhaným masem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mini burgery a hot dogy', minOrder: 10 },
      { id: 'gr14', name: 'Mini hamburger kuřecí', price: 95, amount: '1 ks', description: 'Mini hamburger kuřecí', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mini burgery a hot dogy', minOrder: 10 },
      { id: 'gr15', name: 'Mini hamburger s grilovaným hermelínem', price: 95, amount: '1 ks', description: 'Mini hamburger s grilovaným hermelínem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Mini burgery a hot dogy', minOrder: 10 },
      { id: 'gr16', name: 'Hot dog', price: 69, amount: '1 ks', description: 'Hot dog', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mini burgery a hot dogy', minOrder: 10 },
      // Maso a speciality
      { id: 'gr17', name: 'Marinovaná vepřová krkovice', price: 550, amount: '1 kg', description: 'Marinovaná vepřová krkovice', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr18', name: 'Kuřecí stehenní steak', price: 495, amount: '1 kg', description: 'Kuřecí stehenní steak', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr19', name: 'Marinované kuřecí prso v bylinkách', price: 530, amount: '1 kg', description: 'Marinované kuřecí prso v bylinkách', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr20', name: 'Naložená kuřecí křídla', price: 395, amount: '1 kg', description: 'Naložená kuřecí křídla', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr21', name: 'Masový špíz', price: 550, amount: '1 kg', description: 'Kuřecí, vepřové, cibule, paprika', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr22', name: 'Slezská krkovice', price: 595, amount: '1 kg', description: 'Anglická slanina, cibule (cca 2,5kg)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr23', name: 'Selečí roláda', price: 720, amount: '1 kg', description: 'Selečí roláda (cca 2,5kg)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr24', name: 'Grilovaná staročeská klobása', price: 445, amount: '1 kg', description: 'Grilovaná staročeská klobása', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr25', name: 'Grilovaná makrela', price: 695, amount: '1 kg', description: 'Grilovaná makrela', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      { id: 'gr26', name: 'Grilovaný pstruh', price: 895, amount: '1 kg', description: 'Grilovaný pstruh', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Maso a speciality', minOrder: 1 },
      // Co k tomu?
      { id: 'gr27', name: 'Grilované brambory Grenaille', price: 195, amount: '1 kg', description: 'Grilované brambory Grenaille', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr28', name: 'Salát Coleslaw', price: 305, amount: '1 kg', description: 'Salát Coleslaw', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr29', name: 'Řecké Tzatziki', price: 345, amount: '1 kg', description: 'Řecké Tzatziki', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr30', name: 'Lehký bramborový salát', price: 295, amount: '1 kg', description: 'Lehký bramborový salát', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr31', name: 'Těstovinový salát se zeleninou', price: 320, amount: '1 kg', description: 'Těstovinový salát se zeleninou', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr32', name: 'Míchaný zeleninový salát', price: 355, amount: '1 kg', description: 'Míchaný zeleninový salát', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr33', name: 'Nakládaná zelenina', price: 315, amount: '1 kg', description: 'Nakládaná zelenina', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr34', name: 'Dressingy a studené omáčky dle nabídky', price: 105, amount: '0,5 l', description: 'Dressingy a studené omáčky dle nabídky', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Co k tomu?', minOrder: 1 },
      { id: 'gr35', name: 'Variace pečiva', price: 25, amount: '1 osoba', description: 'Variace pečiva / 1 osoba', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Co k tomu?', minOrder: 1 },
    ],
    'teply-bufet': [
      // Masové pokrmy
      { id: 'tb1', name: 'BBQ wings (kuřecí křídla)', price: 395, amount: '1 kg', description: 'BBQ wings (kuřecí křídla)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'tb2', name: 'Domácí pečená sekaná', price: 395, amount: '1 kg', description: 'Domácí pečená sekaná', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'tb3', name: 'Filírovaná panenka v citronovém pepři', price: 690, amount: '1 kg', description: 'Filírovaná panenka v citronovém pepři', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'tb4', name: 'Filírované kuřecí prso v marinádě', price: 495, amount: '1 kg', description: 'Filírované kuřecí prso v marinádě', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'tb5', name: 'Filírovaný flank steak', price: 730, amount: '1 kg', description: 'Filírovaný flank steak', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      // Guláše
      { id: 'tb6', name: 'Hovězí guláš', price: 115, amount: '100 g', description: 'Hovězí guláš', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Guláše', minOrder: 10 },
      { id: 'tb7', name: 'Vepřový maďarský guláš', price: 95, amount: '100 g', description: 'Vepřový maďarský guláš', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Guláše', minOrder: 10 },
      { id: 'tb8', name: 'Zvěřinový guláš', price: 115, amount: '100 g', description: 'Zvěřinový guláš (jelení, srnčí, dančí, divočák)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Guláše', minOrder: 10 },
      // And more menu items from the teplý bufet section...
      { id: 'tb9', name: 'Hot dogy', price: 69, amount: '1 ks', description: 'Hot dogy', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 10 },
      { id: 'tb10', name: 'Krůtí perkelt, čerstvá zelenina', price: 105, amount: '100 g', description: 'Krůtí perkelt, čerstvá zelenina', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 10 },
    ],
    // Continue with more sections
    'korytka': [
      { id: 'ko1', name: 'Tradiční korýtko', price: 2300, amount: '1 ks', description: 'Celková váha 4,85kg - Mini kuřecí řízečky, Mini vepřové řízečky, Babiččina domácí sekaná, Masové špízky, Moravské uzené, Sýrové korbačíky, Salát Coleslaw, Pečené brambůrky, Nakládaná zelenina, Čerstvá zelenina, Studené omáčky (2 druhy), Pečivo', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Korýtka', minOrder: 1 },
      { id: 'ko2', name: 'Smažené korýtko', price: 2500, amount: '1 ks', description: 'Celková váha 4,3kg - Mini kuřecí řízečky, Mini vepřové řízečky, Smažené sýrové tyčinky, Smažený Camembert, Smažený květák, Smažené cibulové kroužky, Domácí bramborové chipsy, Čerstvá zelenina, Studené omáčky (2 druhy), Pečivo', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Korýtka', minOrder: 1 },
      { id: 'ko3', name: 'Masové korýtko', price: 2500, amount: '1 ks', description: 'Celková váha 5,5kg - Vepřové koleno - pečené, Masová žebírka - marinovaná, Česneková bok - pečený, Kuřecí křidélka - grilovaná, Domácí klobása - pečená, Salát z kysaným zelím a špekem, Pečené brambůrky, Nakládaná zelenina, Čerstvá zelenina, Smetanový křen, Hořčice, Pečivo', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Korýtka', minOrder: 1 },
      { id: 'ko4', name: 'Teenager korýtko', price: 2300, amount: '1 ks', description: 'Celková váha 4kg - Mini burger hovězí (kuřecí), Tortilla blue cheese 8x, Kuřecí stripsy, Domácí Nachos, Domácí rajčatová salsa, Smažené hranolky', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Korýtka', minOrder: 1 },
      { id: 'ko5', name: 'Vegetarián korýtko', price: 2300, amount: '1 ks', description: 'Celková váha 4kg - Cizrnové ragú, Grilované cuketové hranolky, Smažený květák, Zlatý kozí sýr, Mini zeláky, Gratinované žampiony s nivou, Pečené brambůrky, Bylinkový dip, Čerstvá zelenina', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Korýtka', minOrder: 1 },
      { id: 'ko6', name: 'Moravské korýtko', price: 2500, amount: '1 ks', description: 'Celková váha 7kg - Pomalu pečená vepřová krkovička, Červené zelí se skořicí, Restované zelí se špekem, Slezské bílé zelí, Bramborové knedlíky, Karlovarské knedlíky, Houskové knedlíky, Cibulový výpek', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Korýtka', minOrder: 1 },
    ],
    'dezerty': [
      { id: 'de1', name: 'Citronový dort', price: 495, amount: '1 ks', description: 'Citronový dort', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 1 },
      { id: 'de2', name: 'Koláč různé druhy náplní', price: 35, amount: '1 ks', description: 'Koláč různé druhy náplní', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 1 },
      { id: 'de3', name: 'Kokosový s mandarinkami', price: 495, amount: '1 ks', description: 'Kokosový s mandarinkami', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 1 },
      { id: 'de4', name: 'Krémové domácí dezerty (mix 60ml)', price: 45, amount: '1 ks', description: 'Krémové domácí dezerty', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 1 },
      { id: 'de5', name: 'Krémové domácí dezerty (mix 100ml)', price: 65, amount: '1 ks', description: 'Krémové domácí dezerty', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 1 },
      { id: 'de6', name: 'Krémeš, smetanový krém', price: 69, amount: '1 ks', description: 'Krémeš, smetanový krém', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 10 },
      { id: 'de7', name: 'Lyonský dort', price: 495, amount: '1 ks', description: 'Čokoláda, banán, oříšky', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty', minOrder: 1 },
      { id: 'de8', name: 'Jablečný závin', price: 285, amount: '1 ks', description: 'Jablečný závin (cca 900g)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty - Záviny', minOrder: 1 },
      { id: 'de9', name: 'Makový závin', price: 315, amount: '1 ks', description: 'Makový závin (cca 900g)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty - Záviny', minOrder: 1 },
      { id: 'de10', name: 'Tvarohový závin', price: 285, amount: '1 ks', description: 'Tvarohový závin (cca 900g)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Dezerty - Záviny', minOrder: 1 },
      // Ovoce
      { id: 'de11', name: 'Ovocná mísa - lokální', price: 330, amount: '1 kg', description: 'Ovocná mísa z lokálního ovoce', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ovoce', minOrder: 1 },
      { id: 'de12', name: 'Ovocná mísa - z exotického ovoce', price: 465, amount: '1 kg', description: 'Ovocná mísa z exotického ovoce', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ovoce', minOrder: 1 },
      { id: 'de13', name: 'Ovocný salát - lokální', price: 450, amount: '1 kg', description: 'Ovocný salát z lokálního ovoce', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ovoce', minOrder: 1 },
      { id: 'de14', name: 'Ovocný salát - z exotického ovoce', price: 540, amount: '1 kg', description: 'Ovocný salát z exotického ovoce', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ovoce', minOrder: 1 },
    ],
    'sluzby': [
      // Příprava stolů
      { id: 'sl1', name: 'Příprava stolů do 39 osob', price: 1500, amount: '1 ks', description: 'Cena zahrnuje rozmístění stolů a židlí včetně založení inventáře', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Příprava stolů', minOrder: 1 },
      { id: 'sl2', name: 'Příprava stolů 40-79 osob', price: 2500, amount: '1 ks', description: 'Cena zahrnuje rozmístění stolů a židlí včetně založení inventáře', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Příprava stolů', minOrder: 1 },
      { id: 'sl3', name: 'Příprava stolů 80 osob a více', price: 0, amount: '1 ks', description: 'Dle domluvy - Cena zahrnuje rozmístění stolů a židlí včetně založení inventáře', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Příprava stolů', minOrder: 1 },
      // Příprava výzdoby
      { id: 'sl4', name: 'Příprava výzdoby do 49 osob', price: 650, amount: '1 ks', description: 'Příprava výzdoby do 49 osob', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Příprava výzdoby', minOrder: 1 },
      { id: 'sl5', name: 'Příprava výzdoby nad 50 osob', price: 1500, amount: '1 ks', description: 'Příprava výzdoby nad 50 osob', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Příprava výzdoby', minOrder: 1 },
      // Ubrusy a potahy
      { id: 'sl6', name: 'Bílý ubrus (220 x 140 cm)', price: 75, amount: '1 ks', description: 'Bílý ubrus (220 x 140 cm)', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ubrusy a potahy', minOrder: 1 },
      { id: 'sl7', name: 'Potah na židle (univerzální)', price: 40, amount: '1 ks', description: 'Potah na židle (univerzální)', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ubrusy a potahy', minOrder: 1 },
      { id: 'sl8', name: 'Stuha na židli', price: 20, amount: '1 ks', description: 'Stuha na židli', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Ubrusy a potahy', minOrder: 1 },
      // And more service items...
      { id: 'sl9', name: 'Personál - Obsluha', price: 200, amount: '1 hod', description: 'Obsluha 1 hod.', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Personál', minOrder: 1 },
      { id: 'sl10', name: 'Personál - Kuchař', price: 250, amount: '1 hod', description: 'Kuchař 1 hod.', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Personál', minOrder: 1 },
      { id: 'sl11', name: 'Personál - Pomocná síla v kuchyni', price: 200, amount: '1 hod', description: 'Pomocná síla v kuchyni 1 hod.', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Personál', minOrder: 1 },
      { id: 'sl12', name: 'Doprava', price: 15, amount: '1 km', description: '15,- až 20,- /1km nebo dle domluvy', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Doprava', minOrder: 1 },
    ],
    'studeny-bufet': [
      // Masové pokrmy
      { id: 'sb1', name: 'Anglický roastbeef', price: 1150, amount: '1 kg', description: 'Anglický roastbeef (min. 1kg)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb2', name: 'Domácí bulharka', price: 375, amount: '1 kg', description: 'Domácí bulharka', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb3', name: 'Domácí paštika s mandlemi', price: 375, amount: '1 kg', description: 'Domácí paštika s mandlemi', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb4', name: 'Domácí tlačenka - drůbeží', price: 390, amount: '1 kg', description: 'Domácí tlačenka - drůbeží', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb5', name: 'Domácí tlačenka - vepřová', price: 390, amount: '1 kg', description: 'Domácí tlačenka - vepřová', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb6', name: 'Medová šunka krájená', price: 445, amount: '0,5 kg', description: 'Medová šunka krájená', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb7', name: 'Pečené švestky v česnekovém boku', price: 155, amount: '100 g', description: 'Pečené švestky v česnekovém boku', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb8', name: 'Tatarák hovězí s topinkami a česnekem', price: 175, amount: '100 g', description: 'Tatarák hovězí s topinkami a česnekem (min. 250g)', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 2.5 },
      { id: 'sb9', name: 'Variace tuzemských uzenin', price: 720, amount: '1 kg', description: 'Variace tuzemských uzenin', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'sb10', name: 'Variace zahraničních uzenin', price: 1150, amount: '1 kg', description: 'Variace zahraničních uzenin', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      
      // Vegetariánské pokrmy
      { id: 'sb11', name: 'Domácí Nachos s rajčatovou salsou', price: 420, amount: '0,75 kg', description: 'Domácí Nachos s rajčatovou salsou', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb12', name: 'Hummus se sušenými rajčaty', price: 335, amount: '1 kg', description: 'Hummus se sušenými rajčaty', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb13', name: 'Hummus s římským kmínem', price: 335, amount: '1 kg', description: 'Hummus s římským kmínem', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb14', name: 'Hummus s uzenou paprikou', price: 335, amount: '1 kg', description: 'Hummus s uzenou paprikou', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb15', name: 'Quiche - cibulový', price: 425, amount: '1 ks', description: 'Quiche - cibulový', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb16', name: 'Quiche - sýrový', price: 425, amount: '1 ks', description: 'Quiche - sýrový', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb17', name: 'Quiche - špenátový', price: 425, amount: '1 ks', description: 'Quiche - špenátový', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb18', name: 'Quiche - zeleninový', price: 425, amount: '1 ks', description: 'Quiche - zeleninový', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb19', name: 'Sýrová mísa', price: 720, amount: '1 kg', description: 'Sýrová mísa', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb20', name: 'Sýrové kuličky', price: 95, amount: '100 g', description: 'Sýrové kuličky', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb21', name: 'Sýrová roláda plněná', price: 790, amount: '1 kg', description: 'Sýrová roláda plněná', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb22', name: 'Špíz Caprese', price: 485, amount: '1 kg', description: 'Cherry rajčátko, mozzarella, bazalka', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb23', name: 'Slané záviny z listového těsta', price: 395, amount: '1 kg', description: 'Slané záviny z listového těsta (různé druhy náplní)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb24', name: 'Tatarák tvarůžkový s topinkami a česnekem', price: 175, amount: '100 g', description: 'Tatarák tvarůžkový s topinkami a česnekem (min. 250g)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 2.5 },
      { id: 'sb25', name: 'Variace tuzemských sýrů', price: 720, amount: '1 kg', description: 'Variace tuzemských sýrů', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'sb26', name: 'Variace zahraničních sýrů', price: 1150, amount: '1 kg', description: 'Variace zahraničních sýrů', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      
      // Rybí pokrmy
      { id: 'sb27', name: 'Gravlax z lososa', price: 185, amount: '100 g', description: 'Gravlax z lososa (min. 500g)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Rybí pokrmy', minOrder: 5 },
      { id: 'sb28', name: 'Míchaný salát s mořskými plody', price: 1350, amount: '1 kg', description: 'Míchaný salát s mořskými plody', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Rybí pokrmy', minOrder: 1 },
      { id: 'sb29', name: 'Míchaný zeleninový salát s uzeným lososem, kapary, rajčata', price: 1190, amount: '1 kg', description: 'Míchaný zeleninový salát s uzeným lososem, kapary, rajčata', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Rybí pokrmy', minOrder: 1 },
      { id: 'sb30', name: 'Quiche s uzeným lososem', price: 520, amount: '1 ks', description: 'Quiche s uzeným lososem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Rybí pokrmy', minOrder: 1 },
      { id: 'sb31', name: 'Tartar (lososový, tuňákový)', price: 185, amount: '100 g', description: 'Tartar (lososový, tuňákový) (min. 500g)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Rybí pokrmy', minOrder: 5 },
      
      // Mix
      { id: 'sb32', name: 'Chlebíčky (min. 10ks)', price: 35, amount: '1 ks', description: 'Chlebíčky (min. 10ks)', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 10 },
      { id: 'sb33', name: 'Domácích pomazánek', price: 395, amount: '1 kg', description: 'Domácích pomazánek', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
      { id: 'sb34', name: 'Fingerfood', price: 67, amount: '1 ks', description: 'Fingerfood, cena je průměr', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
      { id: 'sb35', name: 'Jednohubek (min. 10ks)', price: 18, amount: '1 ks', description: 'Jednohubek (min. 10ks)', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 10 },
      { id: 'sb36', name: 'Kanapek (min. 10ks)', price: 32, amount: '1 ks', description: 'Kanapek (min. 10ks)', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 10 },
      { id: 'sb37', name: 'Obložené mini bagetky', price: 65, amount: '1 ks', description: 'Obložené mini bagetky', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
      { id: 'sb38', name: 'Plněné croissanty', price: 65, amount: '1 ks', description: 'Plněné croissanty', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
      { id: 'sb39', name: 'Tortilla se zeleninou a kuřecím masem', price: 105, amount: '1 ks', description: 'Tortilla se zeleninou a kuřecím masem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
      { id: 'sb40', name: 'Tortilla se zeleninou a modrým sýrem', price: 95, amount: '1 ks', description: 'Tortilla se zeleninou a modrým sýrem', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
      { id: 'sb41', name: 'Tortilla se zeleninou a vepřovým masem', price: 105, amount: '1 ks', description: 'Tortilla se zeleninou a vepřovým masem', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Mix', minOrder: 1 },
    ],
    'polévky': [
      { id: 'po1', name: 'Kotlíkové - zelná', price: 65, amount: '1 porce', description: 'Kotlíková zelná polévka (min. 10 porcí)', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Polévky', minOrder: 10 },
      { id: 'po2', name: 'Kotlíkové - gulášová', price: 65, amount: '1 porce', description: 'Kotlíková gulášová polévka (min. 10 porcí)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Polévky', minOrder: 10 },
      { id: 'po3', name: 'Kotlíkové - dle domluvy', price: 65, amount: '1 porce', description: 'Kotlíková polévka dle domluvy (min. 10 porcí)', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Polévky', minOrder: 10 },
    ],
    'rauty': [
      // Teplý bufet - masové pokrmy
      { id: 'ra1', name: 'BBQ wings (kuřecí křídla)', price: 395, amount: '1 kg', description: 'BBQ wings (kuřecí křídla)', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra2', name: 'Domácí pečená sekaná', price: 395, amount: '1 kg', description: 'Domácí pečená sekaná', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra3', name: 'Filírovaná panenka v citronovém pepři', price: 690, amount: '1 kg', description: 'Filírovaná panenka v citronovém pepři', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra4', name: 'Filírované kuřecí prso v marinádě', price: 495, amount: '1 kg', description: 'Filírované kuřecí prso v marinádě', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra5', name: 'Filírovaný flank steak', price: 730, amount: '1 kg', description: 'Filírovaný flank steak', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra6', name: 'Kuřecí paličky na medu', price: 430, amount: '1 kg', description: 'Kuřecí paličky na medu', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra7', name: 'Marinovaná vepřová žebírka', price: 575, amount: '1 kg', description: 'Marinovaná vepřová žebírka', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra8', name: 'Masové kuličky (Meat balls mix)', price: 445, amount: '1 kg', description: 'Masové kuličky (Meat balls mix)', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra9', name: 'Řecké biftečky plněné Fetou', price: 525, amount: '1 kg', description: 'Řecké biftečky plněné Fetou', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      { id: 'ra10', name: 'Smažené mini řízečky - holandské', price: 650, amount: '1 kg', description: 'Smažené mini řízečky - holandské', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Masové pokrmy', minOrder: 1 },
      
      // Vegetariánské pokrmy
      { id: 'ra11', name: 'Falafel s jogurtovým dipem', price: 565, amount: '1 kg', description: 'Falafel s jogurtovým dipem', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'ra12', name: 'Mini burger s grilovaným sýrem', price: 105, amount: '1 ks', description: 'Mini burger s grilovaným sýrem (min. 10ks)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 10 },
      { id: 'ra13', name: 'Placičky - bramborové', price: 260, amount: '1 kg', description: 'Placičky - bramborové', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'ra14', name: 'Placičky - luštěninové', price: 300, amount: '1 kg', description: 'Placičky - luštěninové', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'ra15', name: 'Placičky - zeleninové', price: 300, amount: '1 kg', description: 'Placičky - zeleninové', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'ra16', name: 'Placičky - zelné', price: 260, amount: '1 kg', description: 'Placičky - zelné', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'ra17', name: 'Plněné žampiony (různé náplně)', price: 465, amount: '1 kg', description: 'Plněné žampiony (různé náplně)', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      { id: 'ra18', name: 'Ratatouille', price: 405, amount: '1 kg', description: 'Ratatouille', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Vegetariánské pokrmy', minOrder: 1 },
      
      // Ryby
      { id: 'ra20', name: 'Ryby v papilotě - candát', price: 895, amount: '1 kg', description: 'Ryby v papilotě - candát', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra21', name: 'Ryby v papilotě - tilapie', price: 895, amount: '1 kg', description: 'Ryby v papilotě - tilapie', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra22', name: 'Ryby v papilotě - mořský vlk', price: 1495, amount: '1 kg', description: 'Ryby v papilotě - mořský vlk', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra23', name: 'Ryby v papilotě - sumeček africký', price: 1495, amount: '1 kg', description: 'Ryby v papilotě - sumeček africký', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra24', name: 'Smažená Tilapie', price: 895, amount: '1 kg', description: 'Smažená Tilapie', isVegetarian: false, isVegan: false, isGlutenFree: false, category: 'Ryby', minOrder: 1 },
      { id: 'ra25', name: 'Pečená filátka pstruha s citrusy', price: 995, amount: '1 kg', description: 'Pečená filátka pstruha s citrusy', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra26', name: 'Pečený losos na bylinkách', price: 1190, amount: '1 kg', description: 'Pečený losos na bylinkách', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra27', name: 'Plněné kalamáry se špenátem', price: 1150, amount: '1 kg', description: 'Plněné kalamáry se špenátem', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      { id: 'ra28', name: 'Krevetové špízy', price: 1450, amount: '1 kg', description: 'Krevetové špízy', isVegetarian: false, isVegan: false, isGlutenFree: true, category: 'Ryby', minOrder: 1 },
      
      // Přílohy
      { id: 'ra29', name: 'Bramborovo-karotkové pyré', price: 215, amount: '1 kg', description: 'Bramborovo-karotkové pyré', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra30', name: 'Bulgur s bylinkami', price: 215, amount: '1 kg', description: 'Bulgur s bylinkami', isVegetarian: true, isVegan: true, isGlutenFree: false, category: 'Přílohy', minOrder: 1 },
      { id: 'ra31', name: 'Celerové pyré', price: 215, amount: '1 kg', description: 'Celerové pyré', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra32', name: 'Česnekové bramboráčky', price: 260, amount: '1 kg', description: 'Česnekové bramboráčky', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Přílohy', minOrder: 1 },
      { id: 'ra33', name: 'Gratinovaná plněná zelenina', price: 415, amount: '1 kg', description: 'Gratinovaná plněná zelenina (cuketa, lilek, paprika, rajče)', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra34', name: 'Grilovaná zelenina na bylinkách', price: 355, amount: '1 kg', description: 'Grilovaná zelenina na bylinkách', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra35', name: 'Jemná bramborová kaše', price: 215, amount: '1 kg', description: 'Jemná bramborová kaše', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra36', name: 'Knedlík - bramborový', price: 215, amount: '1 kg', description: 'Knedlík - bramborový', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Přílohy', minOrder: 1 },
      { id: 'ra37', name: 'Knedlík - houskový', price: 195, amount: '1 kg', description: 'Knedlík - houskový', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Přílohy', minOrder: 1 },
      { id: 'ra38', name: 'Knedlík - karlovarský', price: 195, amount: '1 kg', description: 'Knedlík - karlovarský', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Přílohy', minOrder: 1 },
      { id: 'ra39', name: 'Pečené brambory Grenaille', price: 195, amount: '1 kg', description: 'Pečené brambory Grenaille', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra40', name: 'Plněné žampiony s modrým sýrem', price: 465, amount: '1 kg', description: 'Plněné žampiony s modrým sýrem', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra41', name: 'Steakové hranolky', price: 260, amount: '1 kg', description: 'Steakové hranolky', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
      { id: 'ra42', name: 'Tarhoňa se zeleninou', price: 195, amount: '1 kg', description: 'Tarhoňa se zeleninou', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Přílohy', minOrder: 1 },
      { id: 'ra43', name: 'Zeleninové rizoto', price: 195, amount: '1 kg', description: 'Zeleninové rizoto', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Přílohy', minOrder: 1 },
    ],
    'doplnky': [
      { id: 'dp1', name: 'Variace pečiva', price: 25, amount: '1 osoba', description: 'Variace pečiva (1 osoba)', isVegetarian: true, isVegan: false, isGlutenFree: false, category: 'Doplňky & Omáčky', minOrder: 1 },
      { id: 'dp2', name: 'Mix omáček a dressingů dle nabídky', price: 105, amount: '0,5 l', description: 'Mix omáček a dressingů dle nabídky', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Doplňky & Omáčky', minOrder: 1 },
      { id: 'dp3', name: 'Nakládaná zelenina', price: 315, amount: '1 kg', description: 'Nakládaná zelenina', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Doplňky & Omáčky', minOrder: 1 },
      { id: 'dp4', name: 'Řecké tzatziki', price: 345, amount: '1 kg', description: 'Řecké tzatziki', isVegetarian: true, isVegan: false, isGlutenFree: true, category: 'Doplňky & Omáčky', minOrder: 1 },
      { id: 'dp5', name: 'Pražené mandle', price: 95, amount: '100 g', description: 'Pražené mandle', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Doplňky & Omáčky', minOrder: 1 },
      { id: 'dp6', name: 'Pražené kešu', price: 135, amount: '100 g', description: 'Pražené kešu', isVegetarian: true, isVegan: true, isGlutenFree: true, category: 'Doplňky & Omáčky', minOrder: 1 },
    ],
    // Add all other necessary categories from PDFs
  };

  // Function to filter products based on search query and filters
  const filteredProducts = () => {
    // If "all" category is selected, combine all products from all categories
    let products = activeCategory === 'all' 
      ? Object.values(catalogData).flat() 
      : catalogData[activeCategory] || [];
    
    // Apply search filter
    if (searchQuery) {
      products = products.filter(item => 
        item.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
        item.description.toLowerCase().includes(searchQuery.toLowerCase())
      );
    }
    
    // Apply dietary filters
    if (filters.vegetarian) {
      products = products.filter(item => item.isVegetarian);
    }
    
    if (filters.vegan) {
      products = products.filter(item => item.isVegan);
    }
    
    if (filters.glutenFree) {
      products = products.filter(item => item.isGlutenFree);
    }
    
    // Apply price filter
    products = products.filter(item => 
      item.price >= filters.priceRange[0] && 
      item.price <= filters.priceRange[1]
    );
    
    return products;
  };

  // Function to calculate total price
  const calculateTotal = () => {
    return cart.reduce((total, item) => total + (item.price * item.quantity), 0);
  };

  // Function to add item to cart
  const addToCart = (product) => {
    const existingItem = cart.find(item => item.id === product.id);
    if (existingItem) {
      const updatedCart = cart.map(item => 
        item.id === product.id 
          ? {...item, quantity: item.quantity + 1} 
          : item
      );
      setCart(updatedCart);
    } else {
      setCart([...cart, {...product, quantity: 1}]);
    }
  };

  // Function to remove item from cart
  const removeFromCart = (id) => {
    const existingItem = cart.find(item => item.id === id);
    if (existingItem && existingItem.quantity === 1) {
      setCart(cart.filter(item => item.id !== id));
    } else {
      const updatedCart = cart.map(item => 
        item.id === id 
          ? {...item, quantity: item.quantity - 1} 
          : item
      );
      setCart(updatedCart);
    }
  };

  // Function to clear cart
  const clearCart = () => {
    setCart([]);
  };

  // Function to handle contact form submission
  const handleContactFormSubmit = (e) => {
    e.preventDefault();
    // Here you would typically send the data to a server
    alert('Děkujeme za vaši objednávku. Brzy se vám ozveme.');
    setShowContactForm(false);
  };

  // Function to generate and download PDF
  const generatePDF = () => {
    // Create a virtual element to hold our PDF content
    const printContent = document.createElement('div');
    printContent.className = 'pdf-content';
    
    // Add styling for the PDF
    const style = document.createElement('style');
    style.textContent = `
      .pdf-content {
        font-family: Arial, sans-serif;
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
      }
      .pdf-header {
        text-align: center;
        margin-bottom: 30px;
      }
      .pdf-logo {
        font-size: 24px;
        font-weight: bold;
        margin-bottom: 5px;
        color: #b7981a;
      }
      .pdf-title {
        font-size: 20px;
        margin-bottom: 20px;
        border-bottom: 2px solid #b7981a;
        padding-bottom: 10px;
      }
      .pdf-info {
        display: flex;
        justify-content: space-between;
        margin-bottom: 30px;
      }
      .pdf-customer-info, .pdf-event-info {
        width: 48%;
      }
      .pdf-section-title {
        font-size: 16px;
        font-weight: bold;
        margin-bottom: 10px;
        color: #b7981a;
      }
      .pdf-info-item {
        margin-bottom: 5px;
      }
      .pdf-items {
        width: 100%;
        border-collapse: collapse;
        margin-bottom: 30px;
      }
      .pdf-items th, .pdf-items td {
        border: 1px solid #ddd;
        padding: 10px;
        text-align: left;
      }
      .pdf-items th {
        background-color: #f2f2f2;
      }
      .pdf-items tr:nth-child(even) {
        background-color: #f9f9f9;
      }
      .pdf-total-row {
        font-weight: bold;
      }
      .pdf-notes {
        margin-bottom: 30px;
      }
      .pdf-footer {
        text-align: center;
        font-size: 12px;
        color: #666;
        margin-top: 50px;
        border-top: 1px solid #ddd;
        padding-top: 10px;
      }
    `;
    
    printContent.appendChild(style);
    
    // Header with logo and title
    const header = document.createElement('div');
    header.className = 'pdf-header';
    
    const logo = document.createElement('div');
    logo.className = 'pdf-logo';
    logo.textContent = 'Folk Food Catering';
    
    const subtitle = document.createElement('div');
    subtitle.textContent = 'Chutě které spojují';
    
    const title = document.createElement('div');
    title.className = 'pdf-title';
    title.textContent = 'Objednávka cateringových služeb';
    
    header.appendChild(logo);
    header.appendChild(subtitle);
    header.appendChild(title);
    
    // Information section
    const info = document.createElement('div');
    info.className = 'pdf-info';
    
    // Customer information
    const customerInfo = document.createElement('div');
    customerInfo.className = 'pdf-customer-info';
    
    const customerTitle = document.createElement('div');
    customerTitle.className = 'pdf-section-title';
    customerTitle.textContent = 'Kontaktní údaje';
    
    customerInfo.appendChild(customerTitle);
    
    const customerDetails = [
      { label: 'Jméno:', value: contactInfo.name || 'Nevyplněno' },
      { label: 'E-mail:', value: contactInfo.email || 'Nevyplněno' },
      { label: 'Telefon:', value: contactInfo.phone || 'Nevyplněno' }
    ];
    
    customerDetails.forEach(detail => {
      const item = document.createElement('div');
      item.className = 'pdf-info-item';
      item.textContent = `${detail.label} ${detail.value}`;
      customerInfo.appendChild(item);
    });
    
    // Event information
    const eventInfo = document.createElement('div');
    eventInfo.className = 'pdf-event-info';
    
    const eventTitle = document.createElement('div');
    eventTitle.className = 'pdf-section-title';
    eventTitle.textContent = 'Detaily akce';
    
    eventInfo.appendChild(eventTitle);
    
    const eventDetails = [
      { label: 'Datum:', value: contactInfo.eventDate || 'Nevyplněno' },
      { label: 'Čas:', value: contactInfo.eventTime || 'Nevyplněno' },
      { label: 'Typ akce:', value: contactInfo.eventType || 'Nevyplněno' },
      { label: 'Počet osob:', value: contactInfo.guests || 'Nevyplněno' }
    ];
    
    eventDetails.forEach(detail => {
      const item = document.createElement('div');
      item.className = 'pdf-info-item';
      item.textContent = `${detail.label} ${detail.value}`;
      eventInfo.appendChild(item);
    });
    
    info.appendChild(customerInfo);
    info.appendChild(eventInfo);
    
    // Order items table
    const itemsTitle = document.createElement('div');
    itemsTitle.className = 'pdf-section-title';
    itemsTitle.textContent = 'Objednané položky';
    
    const table = document.createElement('table');
    table.className = 'pdf-items';
    
    // Table header
    const thead = document.createElement('thead');
    const headerRow = document.createElement('tr');
    
    ['Položka', 'Množství', 'Jednotka', 'Cena/ks', 'Celkem'].forEach(text => {
      const th = document.createElement('th');
      th.textContent = text;
      headerRow.appendChild(th);
    });
    
    thead.appendChild(headerRow);
    table.appendChild(thead);
    
    // Table body
    const tbody = document.createElement('tbody');
    
    // Add each cart item to the table
    cart.forEach(item => {
      const row = document.createElement('tr');
      
      const nameCell = document.createElement('td');
      nameCell.textContent = item.name;
      
      const quantityCell = document.createElement('td');
      quantityCell.textContent = item.quantity;
      
      const unitCell = document.createElement('td');
      unitCell.textContent = item.amount;
      
      const priceCell = document.createElement('td');
      priceCell.textContent = `${item.price} Kč`;
      
      const totalCell = document.createElement('td');
      totalCell.textContent = `${item.price * item.quantity} Kč`;
      
      row.appendChild(nameCell);
      row.appendChild(quantityCell);
      row.appendChild(unitCell);
      row.appendChild(priceCell);
      row.appendChild(totalCell);
      
      tbody.appendChild(row);
    });
    
    // Add total row
    const totalRow = document.createElement('tr');
    totalRow.className = 'pdf-total-row';
    
    const totalLabelCell = document.createElement('td');
    totalLabelCell.colSpan = 4;
    totalLabelCell.textContent = 'Celkem:';
    totalLabelCell.style.textAlign = 'right';
    
    const totalValueCell = document.createElement('td');
    totalValueCell.textContent = `${calculateTotal()} Kč`;
    
    totalRow.appendChild(totalLabelCell);
    totalRow.appendChild(totalValueCell);
    
    tbody.appendChild(totalRow);
    table.appendChild(tbody);
    
    // Notes section if there are special requirements
    if (contactInfo.specialRequirements) {
      const notesTitle = document.createElement('div');
      notesTitle.className = 'pdf-section-title';
      notesTitle.textContent = 'Speciální požadavky';
      
      const notes = document.createElement('div');
      notes.className = 'pdf-notes';
      notes.textContent = contactInfo.specialRequirements;
      
      printContent.appendChild(notesTitle);
      printContent.appendChild(notes);
    }
    
    // Footer
    const footer = document.createElement('div');
    footer.className = 'pdf-footer';
    footer.innerHTML = 'Folk Food Catering | Tel: +420 731 407 330 | Web: folkfoodcatering.cz<br>Nabídka je platná 14 dní od vytvoření.';
    
    // Append all sections to the main container
    printContent.appendChild(header);
    printContent.appendChild(info);
    printContent.appendChild(itemsTitle);
    printContent.appendChild(table);
    printContent.appendChild(footer);
    
    // Append to document body (hidden)
    printContent.style.display = 'none';
    document.body.appendChild(printContent);
    
    // Create a new window for printing
    const printWindow = window.open('', '_blank');
    
    // Write the content to the new window
    printWindow.document.write(`
      <!DOCTYPE html>
      <html>
      <head>
        <title>Folk Food Catering - Objednávka</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
      </head>
      <body>
        ${printContent.outerHTML}
        <script>
          window.onload = function() {
            window.print();
            // Close the window after printing (uncomment if desired)
            // setTimeout(function() { window.close(); }, 500);
          }
        </script>
      </body>
      </html>
    `);
    
    // Remove the temporary element from the DOM
    document.body.removeChild(printContent);
  };

  // Return the UI
  return (
    <div className="w-full max-w-7xl mx-auto p-4">
      <header className="mb-6">
        <div className="flex items-center justify-between">
          <div>
            <h1 className="text-3xl font-bold text-yellow-800">Folk Food Catering</h1>
            <p className="text-lg text-gray-600">Chutě které spojují</p>
          </div>
          <div className="flex space-x-2">
            <Button 
              onClick={() => setShowCart(!showCart)}
              className={`flex items-center ${showCart ? 'bg-yellow-700' : 'bg-yellow-600'} hover:bg-yellow-700`}
            >
              <ShoppingCart className="mr-2 h-5 w-5" />
              <span>{cart.length > 0 ? `${cart.length} položek` : 'Košík'}</span>
            </Button>
          </div>
        </div>
      </header>

      <main className="flex flex-col md:flex-row gap-6">
        {/* Left column - Categories and filters */}
        <div className="w-full md:w-1/4">
          <Card className="mb-4">
            <CardContent className="p-4">
              <div className="mb-4">
                <div className="relative">
                  <Search className="absolute left-2 top-2.5 h-4 w-4 text-gray-500" />
                  <Input 
                    placeholder="Hledat v nabídce..."
                    className="pl-8"
                    value={searchQuery}
                    onChange={(e) => setSearchQuery(e.target.value)}
                  />
                </div>
              </div>

              <div className="mb-4">
                <h3 className="font-medium mb-2 flex items-center">
                  <Filter className="mr-2 h-4 w-4" /> Filtry
                </h3>
                <div className="space-y-2">
                  <div className="flex items-center space-x-2">
                    <Checkbox 
                      id="vegetarian" 
                      checked={filters.vegetarian}
                      onCheckedChange={(checked) => setFilters({...filters, vegetarian: !!checked})}
                    />
                    <Label htmlFor="vegetarian">Vegetariánské</Label>
                  </div>
                  <div className="flex items-center space-x-2">
                    <Checkbox 
                      id="vegan" 
                      checked={filters.vegan}
                      onCheckedChange={(checked) => setFilters({...filters, vegan: !!checked})}
                    />
                    <Label htmlFor="vegan">Veganské</Label>
                  </div>
                  <div className="flex items-center space-x-2">
                    <Checkbox 
                      id="glutenFree" 
                      checked={filters.glutenFree}
                      onCheckedChange={(checked) => setFilters({...filters, glutenFree: !!checked})}
                    />
                    <Label htmlFor="glutenFree">Bez lepku</Label>
                  </div>
                </div>
              </div>

              <div>
                <h3 className="font-medium mb-2">Kategorie</h3>
                <div className="grid grid-cols-2 md:grid-cols-4 gap-2">
                  {categories.map((category) => (
                    <Button 
                      key={category.id}
                      variant={activeCategory === category.id ? "default" : "outline"}
                      className={`w-full justify-start text-left transition-all duration-200 text-sm ${
                        activeCategory === category.id 
                          ? 'bg-yellow-600 hover:bg-yellow-700 text-white font-medium shadow-md' 
                          : 'hover:bg-yellow-50 hover:text-yellow-700 border-yellow-100'
                      }`}
                      onClick={() => setActiveCategory(category.id)}
                    >
                      <span className="mr-2">{category.icon}</span>
                      {category.name}
                    </Button>
                  ))}
                </div>
              </div>
            </CardContent>
          </Card>
        </div>

        {/* Right column - Product list and cart */}
        <div className="w-full md:w-3/4">
          {/* Products section */}
          {!showCart && !showContactForm && (
            <div>
              <h2 className="text-2xl font-bold mb-4">
                {categories.find(cat => cat.id === activeCategory)?.name || 'Produkty'}
              </h2>
              
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                {filteredProducts().map((product) => (
                  <Card key={product.id} className="overflow-hidden hover:shadow-lg transition-shadow duration-300 border-yellow-100">
                    <CardContent className="p-4">
                      <div className="flex justify-between items-start mb-2">
                        <h3 className="font-bold text-gray-800">{product.name}</h3>
                        <span className="font-semibold text-yellow-700 bg-yellow-50 px-2 py-1 rounded-md">{product.price} Kč</span>
                      </div>
                      
                      <p className="text-sm text-gray-600 mb-2">{product.description}</p>
                      
                      <div className="flex justify-between items-center">
                        <span className="text-sm bg-gray-100 px-2 py-1 rounded">{product.amount}</span>
                        <div className="flex items-center">
                          <span className="text-xs mr-2 text-gray-600">Min. objednávka: {product.minOrder}</span>
                          <Button 
                            size="sm"
                            onClick={() => addToCart(product)}
                            className="bg-yellow-600 hover:bg-yellow-700 transition-colors duration-200"
                          >
                            <Plus className="h-4 w-4" />
                          </Button>
                        </div>
                      </div>
                      
                      <div className="flex flex-wrap mt-2 gap-1">
                        <span className="bg-gray-100 text-gray-800 text-xs font-medium px-2 py-0.5 rounded">{product.category}</span>
                        {product.isVegetarian && (
                          <span className="bg-green-100 text-green-800 text-xs font-medium px-2 py-0.5 rounded flex items-center">
                            <span className="mr-1">🥬</span>Vegetariánské
                          </span>
                        )}
                        {product.isVegan && (
                          <span className="bg-green-100 text-green-800 text-xs font-medium px-2 py-0.5 rounded flex items-center">
                            <span className="mr-1">🌱</span>Veganské
                          </span>
                        )}
                        {product.isGlutenFree && (
                          <span className="bg-blue-100 text-blue-800 text-xs font-medium px-2 py-0.5 rounded flex items-center">
                            <span className="mr-1">🌾</span>Bez lepku
                          </span>
                        )}
                      </div>
                    </CardContent>
                  </Card>
                ))}
              </div>
              
              {filteredProducts().length === 0 && (
                <div className="text-center py-8">
                  <p>Nebyly nalezeny žádné položky odpovídající vašemu filtru.</p>
                </div>
              )}
            </div>
          )}
          
          {/* Cart section */}
          {showCart && !showContactForm && (
            <div>
              <div className="flex justify-between items-center mb-4">
                <h2 className="text-2xl font-bold">Váš košík</h2>
                <Button 
                  variant="outline"
                  onClick={() => setShowCart(false)}
                >
                  Zpět k nabídce
                </Button>
              </div>
              
              {cart.length === 0 ? (
                <div className="text-center py-8">
                  <p>Váš košík je prázdný.</p>
                  <Button 
                    onClick={() => setShowCart(false)}
                    className="mt-4 bg-yellow-600 hover:bg-yellow-700"
                  >
                    Procházet nabídku
                  </Button>
                </div>
              ) : (
                <>
                  <Card>
                    <CardContent className="p-4">
                      <div className="space-y-4">
                        {cart.map((item) => (
                          <div key={item.id} className="flex justify-between items-center pb-4 border-b">
                            <div>
                              <h3 className="font-medium">{item.name}</h3>
                              <p className="text-sm text-gray-600">{item.amount} × {item.quantity}</p>
                            </div>
                            <div className="flex items-center">
                              <span className="font-semibold mr-4">{item.price * item.quantity} Kč</span>
                              <div className="flex items-center space-x-2">
                                <Button 
                                  size="sm" 
                                  variant="outline"
                                  onClick={() => removeFromCart(item.id)}
                                >
                                  <Minus className="h-4 w-4" />
                                </Button>
                                <span>{item.quantity}</span>
                                <Button 
                                  size="sm"
                                  onClick={() => addToCart(item)}
                                  className="bg-yellow-600 hover:bg-yellow-700"
                                >
                                  <Plus className="h-4 w-4" />
                                </Button>
                              </div>
                            </div>
                          </div>
                        ))}
                      </div>
                      
                      <div className="mt-6 flex justify-between items-center font-bold text-lg">
                        <span>Celkem:</span>
                        <span>{calculateTotal()} Kč</span>
                      </div>
                      
                      <div className="mt-6 flex justify-between">
                        <Button 
                          variant="outline"
                          onClick={clearCart}
                        >
                          <X className="mr-2 h-4 w-4" /> Vyprázdnit košík
                        </Button>
                        <div className="space-x-2">
                          <Button 
                            onClick={generatePDF}
                            variant="outline"
                            className="flex items-center"
                          >
                            <FileText className="mr-2 h-4 w-4" /> Export PDF
                          </Button>
                          <Button 
                            onClick={() => setShowContactForm(true)}
                            className="bg-yellow-600 hover:bg-yellow-700"
                          >
                            Pokračovat
                          </Button>
                        </div>
                      </div>
                    </CardContent>
                  </Card>
                </>
              )}
            </div>
          )}
          
          {/* Contact form section */}
          {showContactForm && (
            <div>
              <div className="flex justify-between items-center mb-4">
                <h2 className="text-2xl font-bold">Dokončení objednávky</h2>
                <Button 
                  variant="outline"
                  onClick={() => setShowContactForm(false)}
                >
                  Zpět ke košíku
                </Button>
              </div>
              
              <Card>
                <CardContent className="p-4">
                  <form onSubmit={handleContactFormSubmit} className="space-y-4">
                    <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                      <div>
                        <Label htmlFor="name">Jméno a příjmení</Label>
                        <Input 
                          id="name" 
                          required 
                          value={contactInfo.name}
                          onChange={(e) => setContactInfo({...contactInfo, name: e.target.value})}
                        />
                      </div>
                      <div>
                        <Label htmlFor="email">E-mail</Label>
                        <Input 
                          id="email" 
                          type="email" 
                          required 
                          value={contactInfo.email}
                          onChange={(e) => setContactInfo({...contactInfo, email: e.target.value})}
                        />
                      </div>
                      <div>
                        <Label htmlFor="phone">Telefon</Label>
                        <Input 
                          id="phone" 
                          required 
                          value={contactInfo.phone}
                          onChange={(e) => setContactInfo({...contactInfo, phone: e.target.value})}
                        />
                      </div>
                      <div>
                        <Label htmlFor="guests">Počet osob</Label>
                        <Input 
                          id="guests" 
                          type="number" 
                          required 
                          value={contactInfo.guests}
                          onChange={(e) => setContactInfo({...contactInfo, guests: e.target.value})}
                        />
                      </div>
                      <div>
                        <Label htmlFor="eventDate">Datum akce</Label>
                        <Input 
                          id="eventDate" 
                          type="date" 
                          required 
                          value={contactInfo.eventDate}
                          onChange={(e) => setContactInfo({...contactInfo, eventDate: e.target.value})}
                        />
                      </div>
                      <div>
                        <Label htmlFor="eventTime">Čas akce</Label>
                        <Input 
                          id="eventTime" 
                          type="time" 
                          required 
                          value={contactInfo.eventTime}
                          onChange={(e) => setContactInfo({...contactInfo, eventTime: e.target.value})}
                        />
                      </div>
                      <div>
                        <Label htmlFor="eventType">Typ akce</Label>
                        <Select 
                          value={contactInfo.eventType}
                          onValueChange={(value) => setContactInfo({...contactInfo, eventType: value})}
                        >
                          <SelectTrigger>
                            <SelectValue placeholder="Vyberte typ akce" />
                          </SelectTrigger>
                          <SelectContent>
                            <SelectItem value="firemni">Firemní akce</SelectItem>
                            <SelectItem value="svatba">Svatba</SelectItem>
                            <SelectItem value="narozeniny">Narozeninová oslava</SelectItem>
                            <SelectItem value="konference">Konference</SelectItem>
                            <SelectItem value="jine">Jiné</SelectItem>
                          </SelectContent>
                        </Select>
                      </div>
                      <div className="md:col-span-2">
                        <Label htmlFor="specialRequirements">Speciální požadavky nebo poznámky</Label>
                        <textarea 
                          id="specialRequirements"
                          className="w-full min-h-[100px] p-2 border rounded-md"
                          value={contactInfo.specialRequirements}
                          onChange={(e) => setContactInfo({...contactInfo, specialRequirements: e.target.value})}
                        ></textarea>
                      </div>
                    </div>
                    
                    <div className="pt-4 border-t">
                      <h3 className="font-semibold mb-2">Přehled objednávky</h3>
                      <div className="max-h-40 overflow-y-auto mb-4">
                        {cart.map((item) => (
                          <div key={item.id} className="flex justify-between py-1">
                            <span>{item.name} × {item.quantity}</span>
                            <span>{item.price * item.quantity} Kč</span>
                          </div>
                        ))}
                      </div>
                      <div className="flex justify-between font-bold">
                        <span>Celková cena:</span>
                        <span>{calculateTotal()} Kč</span>
                      </div>
                    </div>
                    
                    <div className="flex justify-end space-x-2 pt-4">
                      <Button 
                        type="button"
                        variant="outline"
                        onClick={() => setShowContactForm(false)}
                      >
                        Zpět
                      </Button>
                      <Button 
                        type="button"
                        variant="outline"
                        onClick={generatePDF}
                        className="flex items-center"
                      >
                        <FileText className="mr-2 h-4 w-4" /> Export do PDF
                      </Button>
                      <Button 
                        type="submit"
                        className="bg-yellow-600 hover:bg-yellow-700"
                      >
                        Odeslat objednávku
                      </Button>
                    </div>
                  </form>
                </CardContent>
              </Card>
            </div>
          )}
        </div>
      </main>
      
      <footer className="mt-8 pt-6 border-t text-center text-gray-600">
        <p>© 2025 Folk Food Catering | Tel: +420 731 407 330 | Web: folkfoodcatering.cz | Instagram: folk_food_catering</p>
      </footer>
    </div>
  );
};

export default CateringConfigurator;
