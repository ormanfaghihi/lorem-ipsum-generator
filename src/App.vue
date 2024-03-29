<script setup>
import {computed, reactive, ref} from 'vue'

const inputs = reactive({
  lang: 'en',
  type: 'paragraph',
  n: 2,
  isTrainy: false,
  isUnintelligible: false,
})
const wordResources = reactive({
  en: [
    'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad delectus et nulla odio, repellat reprehenderit.',
    'Dolorum earum minima officiis placeat sapiente unde voluptate?',
    'Delectus, dolor ea earum facilis ipsa perspiciatis!',
    'Lorem ipsum dolor sit amet, consectetur adipisicing elit.',
    'Adipisci cupiditate delectus impedit in incidunt minus porro praesentium voluptatem! Asperiores consequatur consequuntur dolorem et, incidunt pariatur praesentium quae quibusdam quisquam voluptatem.'
  ],
  fa: [
    'لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده از طراحان گرافیک است.',
    'چاپگرها و متون بلکه روزنامه و مجله در ستون و سطر آن چنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز و کاربردهای متنوع با هدف بهبود ابزارهای کاربردی می‌باشد.',
    'کتابهای زیادی در شصت و سه درصد گذشته، حال و آینده شناخت فراوان جامعه و متخصصان را می‌طلبد تا با نرم‌افزارها شناخت بیشتری را برای طراحان رایانه ای علی‌الخصوص طراحان خلاقی و فرهنگ پیشرو در زبان فارسی ایجاد کرد.',
    'در این صورت می‌توان امید داشت که تمام و دشواری موجود در ارائه راهکارها و شرایط سخت تایپ به پایان رسد و زمان مورد نیاز شامل حروفچینی دستاوردهای اصلی و جوابگوی سوالات پیوسته اهل دنیای موجود طراحی اساساً مورد استفاده قرار گیرد.',
    'کتابهای زیادی در شصت و سه درصد گذشته، حال و آینده شناخت فراوان جامعه و متخصصان را می طلبد تا با نرم افزارها شناخت بیشتری را برای طراحان رایانه ای علی الخصوص طراحان خلاقی و فرهنگ پیشرو در زبان فارسی ایجاد کرد. ',
  ],
})

const productResources = reactive({
  en: [
    'Apple 2022 MacBook Air M2 Chip (13-inch, 8GB RAM, 256GB SSD Storage) (QWERTY English) Silver (Renewed Premium)',
    'Early 2020 Apple MacBook Air with 1.1GHz Intel Core i3 (13-inch, 8GB RAM, 256GB SSD Storage) (QWERTY English) Space Gray',
    'Late 2020 Apple MacBook Air with Apple M1 Chip (13.3 inch, 8GB RAM, 256GB SSD) Space Gray',
    'Apple MacBook Pro With Touch Bar Intel Core i5, 13-inch, 8GB RAM, 256GB Storage Space Gray',
    'Apple 2024 MacBook Air 13-inch Laptop with M3 chip: 13.6-inch Liquid Retina Display, 16GB Unified Memory, 512GB SSD Storage, Backlit Keyboard, 1080p FaceTime HD Camera, Touch ID; Starlight',
    'Mid 2017 Apple MacBook Air with 1.8GHz Intel Core i5 (13-inch, 8GB RAM, 256GB SSD) Silver',
    'Apple MacBook Pro MPXQ2LL/A, 13.3 inch Retina Display, 2.3GHz Intel Core i5, 16GB RAM, 256GB SSD, Space Gray',
    'Apple MacBook Air with Intel Core i5, 1.6GHz, (13-inch, 4GB,128GB SSD) - Silver',
    'Apple MacBook Air 13.3-Inch Laptop MD760LL/B, 1.4 GHz Intel i5 Dual Core Processor',
    'Early 2020 Apple MacBook Air with 1.1 GHz Intel Core i5 (13 inch, 8GB RAM, 512GB SSD) Space Gray',
    'Apple 2024 MacBook Air 15-inch Laptop with M3 chip: 15.3-inch Liquid Retina Display, 8GB Unified Memory, 256GB SSD Storage, Backlit Keyboard, 1080p FaceTime HD Camera, Touch ID; Starlight',
    'Apple MacBook Pro 13.3" 2018 256GB MR9Q2LL/A - Space Gray',
    'Apple 2022 MacBook Pro M2 Chip (13-inch, 8GB RAM, 256GB SSD Storage) (QWERTY English) Space Gray (Renewed Premium)',
    'Apple 2023 MacBook Air Laptop with M2 chip: 15.3-inch Liquid Retina Display, 8GB Unified Memory, 256GB SSD Storage, 1080p FaceTime HD Camera, Touch ID. Works with iPhone/iPad; Midnight',
    'Apple 2023 MacBook Pro Laptop M3 Pro chip with 12‑core CPU, 18‑core GPU: 14.2-inch Liquid Retina XDR Display, 18GB Unified Memory, 1TB SSD Storage. Works with iPhone/iPad; Space Black',
    'Apple 13in MacBook Air (2017 Newest Version) 1.8GHz Core i5 CPU, 8GB RAM, 128GB SSD',
    'Apple iPhone 12, 64GB, Blue - Fully Unlocked',
    'Apple iPhone 12 Mini, 64GB, Blue - Unlocked',
    'Apple iPhone SE 2nd Generation, US Version, 64GB, Black - Unlocked',
    'Apple iPhone 11, US Version, 128GB, Purple - Unlocked',
    'Apple iPhone 15, 128GB, Pink - Unlocked',
    'Apple iPhone 12 Pro, 256GB, Graphite - Fully Unlocked',
    'Apple iPhone 13, 128GB, Pink - Unlocked',
    'Apple iPhone XR, 64GB, Black - Unlocked',
    'Apple iPhone 13 Pro, 128GB, Sierra Blue - Unlocked',
    'iPhone 13 Pro Max, 512GB, Graphite - Unlocked',
    'iPhone 13, 128GB, Blue - Unlocked (Renewed Premium)',
    'Apple iPhone 13 Mini, 128GB, Pink - Unlocked',
    'Apple iPhone 11 Pro, US Version, 256GB, Space Gray - Unlocked',
    'Apple iPhone 14 Pro Max, 512GB, Space Black - Unlocked (Renewed Premium)',
    'Apple iPhone 11, 64GB, Purple - Unlocked (Renewed Premium)',
    'Apple iPhone SE 3rd Gen, 64GB, Midnight - Unlocked',
    'Surface Laptop Studio 2 14.4" Touchscreen Convertible (Floating Slider) 2 in 1 Notebook - 2400 x 1600 - Intel Core i7 13th Gen i7-13700H Tetradeca-core (14 Core) - Intel Evo Platform -',
    'Microsoft Surface Pro 9 (2022), 13" 2-in-1 Tablet & Laptop, Thin & Lightweight, Intel 12th Gen i5 Fast Processor, 8GB RAM, 256GB Storage with Windows 11, Copilot, Graphite',
    'Microsoft Surface Laptop 4 13.5” Touch-Screen – AMD Ryzen 5 Surface Edition - 16GB Memory - 256GB Solid State Drive - Platinum',
    'Microsoft Surface Laptop 4 13.5” Touch-Screen – Intel Core i5 - 8GB - 512GB Solid State Drive- Ice Blue',
    'Microsoft Surface Book 2 (Intel Core i7, 8GB RAM, 256GB) - 13.5in',
    'Microsoft Surface Laptop 2, 13.5" Touchscreen Notebook, Intel Core i5-8350U, 16GB RAM, 256 GB SSD, Backlit Keyboard, Display(2256 x 1504), CAM, WiFi, Platinum, Windows 10 Pro(Renewed)',
    'Microsoft Surface Laptop Go - 12.4" Touchscreen - Intel Core i5 - 8GB Memory - 256GB SSD - Platinum',
    'Microsoft OEM System Builder | Windоws 11 Pro | Intended use for new systems | Authorized by Microsoft',
    'New Microsoft Surface Book 3 - 13.5" Touch-Screen - 10th Gen Intel Core i5 - 8GB Memory - 256GB SSD (Latest Model) - Platinum',
    'Audio Dock - Up to 90dB SPL - Two Omni-Directional Microphone arrays - 70Hz ~ 20kHz for Music Playback - Support DP alt Mode, up to Dual Display - Windows 11 Home/Pro, Windows 10, MacOS',
    'Surface Pro 9 (2022), 13" 2-in-1 Tablet & Laptop, Thin & Lightweight, Intel 12th Gen i7 Fast Processor for Multi-Tasking, 16GB RAM, 256GB Storage with Windows 11, Graphite Microsoft Copilot',
    'Surface Go 3 - 10.5" Touchscreen - Intel® Pentium® Gold - 4GB Memory - 64GB eMMC - Device Only - Platinum (Latest Model)',
    'Microsoft Surface Laptop 4 13.5 Touchscreen AMD Ryzen 5 8GB 128GB Windows 11 H, 13-13.99 inches',
    'LifeCam HD-3000 for Business with built-in noise cancelling Microphone, Light Correction, USB Connectivity with universal attachment base, for video calling on Microsoft Teams/Zoom',
    'Microsoft Surface Laptop 3, 13.5" Touchscreen Notebook, Intel Core i5-1035G7, 16GB RAM, 256 GB SSD, Backlit Keyboard, Display(2256 x 1504), CAM, WiFi, Black, Windows 10 Pro(Renewed)',
    'Surface Pro 8 Tablet, i7-1185G7, 16GB RAM, 256GB SSD, 13" Touchscreen Display, Windows 10 Pro Laptop Computer, Graphite Bundled with Black Signature Keyboard, Slim Pen 2 and GizPro USB-C HUB',
    'Surface Laptop 4 15-inch Touchscreen 256GB SSD AMD Ryzen 7 (8GB RAM, Windows 10 Home, Latest Model) - Platinum, 5UI-00001',
    '44W Surface Pro Laptop Charger for Microsoft Surface Pro 3 Pro 4 Pro 5 Pro 6, Laptop 2 1, Go 2 3 Power Supply Cord Computer AC Adapter with 5V 1A USB Charging Port',
    'BMW Brand Style 167 19" E60 E61 M5 E63 E64 M6 Double Spoke Forged Wheels OEM New',
    'BMW F12 F13 F06 M6 OEM Genuine Style 433 20" M Double Spoke Wheels Gloss Turned',
    'EuroActive BMW OEM E70 F15 X5 E71 X6 Y Spoke Style 375 21" Gloss Turned Performance Rims',
    'BMW Brand 2004-2006 E53 X5 OEM White Clear Adaptive Xenon AHL European Lights',
    'BMW OEM F15/F16 X5/X6 Multi-Functional Instrument Cluster Display LCD Retrofit',
    'BMW OEM F10 F12 F13 F06 Multi-Functional Instrument Cluster Display LCD Retrofit',
    'BMW F10 F07 F01 F02 5 & 7 Series OEM 252 Style Radial Spoke 19" Wheels Forged',
    'BMW E70 X5 Genuine Style 177 Cross Spoke 20" Wheel Set',
    'BMW Genuine OEM Clear Headlights and Indicators Z3 2000-2002 New',
    'BMW OEM Genuine Clear Headlights and Indicators Z3 1996-1999',
    'BMW OEM Genuine E60 E61 5 Series 2004-2007 Maple Sycamore Interior Trim Kit',
    'BMW F10 M5 F06 F12 F13 M6 Instrument Cluster Factory Sealed MPH or KMPH OEM',
    'BMW Genuine E90 Portable Euro DVD System',
    'BMW Brand OEM Genuine E53 X5 2000-2006 Style 132 European 19" Wheel Set of 4 New',
    'BMW E90 E90 LCI Sedan 2010+ M3 OEM Side Mirror Assembly Pair Power Fold Version',
    'BMW OEM F23 F23 F87 M Performance Carbon Fiber & Alcantara Interior Trim (LHD)',
    'Mishimoto MMINT-F80-15 Performance Air-to-Water Intercooler Compatible With BMW F8X M3, M4, and M2 2 2015-2020',
    '4X Front Rear Left Right Shock Absorbers w/VDC 37106869019, 37106869021 For BMW X5 G05 RWD xDrive40i 2019-2022',
    'BMW Brand F10 M5 F12 F13 M6 Blue Brembo Front Right Caliper Genuine OEM New',
    'Performance Air to Water Intercooler, Compatible with BMW M5/M6 2012-2016',
    'EuroActive BMW F30 F31 F34 M Performance Carbon Fiber & Alcantara Interior Trim RHD Version',
    'BMW OEM F25 X3 2011+ X26 X4 Rear Camera Factory Retrofit Kit',
    'BMW E39 5 Series 1997-2000 Genuine OEM European Halo Amber Headlamps New',
    'BMW E83 LCI X3 2007-2010 Genuine US Spec Clear Corner Halogen Headlights New',
    'BMW Z4 Genuine Piano Black Wood Dashboard Trim Set New',
    'EuroActive BMW Brand OEM E70 E70 LCI X5 2007+ Performance Alcantara Sport Steering Wheel',
    'Compatible with: BMW F30 F31 F32 F33 F34 F36 F80 F82 Digital Instrumental Cluster Speedometer LED',
    'BMW OEM E82 E90 E60 E63 E70 Bluetooth Module ULF HIGH',
    'T T-ABC New M4 Style Headlamp Compatible with 2005-2012 BMW e90 Headlights 328i 335i xDrive 328xi 335d 335xi 4dr Sedan Accessories Sequential Not Fit ci is 2dr Convertible Coupe (Halogen Ver)',
    '12.3 inch Digital Speedometer Replacement for 2011-2017 BMW 5 Series F10 F11 F18 2010-2017. LCD Digital Gauge Cluster Instrument',
    'for BMW S1000RR 2023 Carbon Fiber Wings with Side Panels Winglets Spoiler Side Fairing Carbon Fiber Bodywork Modification',
    'LED Headlights for 2005-2012 BMW E90/E91 328i/335i/3 Series Headlights Assembly Front Lights Assembly for 4 Doors Sedan BMW,Sequential Turn Signal Low/High Beam DRL Plug & Play (For 05-12 Xenon Ver)',
    'Jun-Star Carbon Fiber F16 Front Bumper Lip Spoiler for BMW X6 F16 xDrive35i xDrive50i M Sport SUV 4-Door 2015-2019 Front Bumper Lip Spoiler Splitters Front Bumper Body Kit Car Accessories for BMW',
    'BMW X5 E70 E70 LCI E71 E72 X6 OEM Tri-Color M Sport Steering Wheel',
    'Headlights for 2005-2012 BMW E90 E91 328i 335i 3-Series 4dr sedan Headlight Assembly with Sequential Turn Signal/Passenger&Driver Side Head Lamp (05-12 Xenon Ver)',
    '12.3 Inch Digital Gauge Cluster Virtual Cockpit for BMW Z4 E89 2009-2018 LCD Instrument Dashboard Speedometer Screen Panel',
    '4 Pcs LED Tail Lights fit for BMW 7 Series F01 F02 2009-2015 led Taillight Upgrade Blink Turn Signal Lights',
    'BMW Brand Genuine M3 E90 E91 E92 E93 Sport Steering Wheel Rim OEM',
    'Indoor Car Cover Replace for 2007-2023 BMW 5 Series, Luxurious Stretch Satin Ultimate Custom-fit Indoor Breathable Car Cover for Dust-Proof, Underground Garage, Car Show (5 Series)',
  ],
  fa: [
    'گوشی موبایل اپل مدل iPhone 13 CH دو سیم‌ کارت ظرفیت 128 گیگابایت و رم 4 گیگابایت - نات اکتیو',
    'گوشی موبایل اپل مدل iPhone 13 CH دو سیم‌ کارت ظرفیت 256 گیگابایت و رم 4 گیگابایت - نات اکتیو',
    'گوشی موبایل اپل مدل iPhone 13 CH دو سیم‌ کارت ظرفیت 128 گیگابایت و رم 4 گیگابایت به همراه شارژر 20 وات اپل - نات اکتیو',
    'گوشی موبایل اپل مدل iPhone 13 Pro Max ZDA تک سیم‌ کارت ظرفیت 256 گیگابایت و رم 6 گیگابایت - نات اکتیو ریفربیش پارت نامبر F',
    'گوشی موبایل اپل مدل iPhone 13 CH دو سیم‌ کارت ظرفیت 256 گیگابایت و رم 4 گیگابایت به همراه شارژر 20 وات اپل - نات اکتیو',
    'گوشی موبایل اپل مدل iPhone 11 ZPA تک سیم‌ کارت ظرفیت 128 گیگابایت و رم 4 گیگابایت',
    'گوشی موبایل اپل مدل iPhone 11 تک سیم‌ کارت ظرفیت 64 گیگابایت و رم 4 گیگابایت - نات اکتیو',
    'گوشی موبایل اپل مدل iPhone 13 Pro Max ZDA تک سیم‌ کارت ظرفیت 128 گیگابایت و رم 6 گیگابایت - نات اکتیو ریفربیش پارت نامبر F',
    'ساعت هوشمند اپل واچ سری SE 2021 مدل  40mm Aluminum Case with Sport silicone Band',
    'ساعت هوشمند اپل واچ مدل Ultra 49 mm Alpine Loop',
    'هدفون بلوتوثی اپل مدل AirPods Pro 2nd Generation',
    'هدفون بلوتوثی اپل مدل AirPods 3',
    'ساعت هوشمند اپل مدل Series 9 Aluminum 45mm M/L',
    'هدفون بلوتوثی اپل مدل AirPods New Generation',
    'تبلت اپل مدل iPad Pro 11 2022 WIFI ظرفیت 128 گیگابایت و رم 8 گیگابایت',
    'تبلت اپل مدل iPad Pro 11 2022 WIFI  ظرفیت 256 گیگابایت و رم 8 گیگابایت',
    'هدفون بلوتوثی اپل مدل AirPods Max',
    'تبلت اپل مدل iPad Air 5th generation Wi-Fi ظرفیت 64 گیگابایت',
    'هدفون بلوتوثی اپل مدل AirPods Pro 2nd Generation 2023 Type-C',
    'ساعت هوشمند اپل مدل Series 8 Aluminum 45mm',
    'لپ تاپ 13.3 اینچی اپل مدل MacBook Air MGN63 2020-M1 8GB 256SSD',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKW3 M2 2023',
    'لپ تاپ 13 اینچی اپل مدل MacBook Air MGND3 2020',
    'لپ تاپ 13.6 اینچی اپل مدل MacBook Air-B M2 2022-M2 8GB 256SSD',
    'لپ تاپ 13.3 اینچی اپل مدل MacBook Air MGN63 2020 LLA-M1 8GB 256SSD',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKP3 M2 2023',
    'لپ تاپ 16.2 اینچی اپل مدل MacBook Pro MRW13 2023-M3 Pro 18GB 512SSD',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKR3 M2 2023',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKT3 M2 2023',
    'لپ تاپ 14.2 اینچی اپل مدل MacBook Pro MTL83 2023-M3 8GB 1SSD',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKV3 2023-M2 8GB 512SSD',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKX3 M2 2023',
    'لپ تاپ 14.2 اینچی اپل مدل MacBook Pro MRX53 2023-M3 Max 36GB 1SSD',
    'لپ تاپ 13.6 اینچ اپل مدل MacBook Air-MLY33 M2 2022 LLA',
    'لپ تاپ 14.2 اینچی اپل مدل MacBook Pro MRX63 2023-M3 Pro 18GB 512SSD',
    'لپ تاپ 13.6 اینچ اپل مدل MacBook Air-MLXY3 M2 2022 LLA',
    'لپ تاپ 14.2 اینچی اپل مدل MacBook Pro MRX43 2023-M3 Pro 18GB 1SSD',
    'لپ تاپ 13.3 اینچی اپل مدل MacBook Pro M2 MNEJ3 2022',
    'لپ تاپ 15.3 اینچی اپل مدل MacBook Air MQKU3 M2 2023',
    'لپ تاپ 14.2 اینچی اپل مدل MacBook Pro MRX73 2023-M3 Pro 18GB 1SSD',
    'چراغ جلو کروز پلاس مدل 401-402 مناسب برای پژو 207 بسته دو عددی',
    'چراغ جلو کروز پلاس مدل 40 مناسب برای پژو 207 بسته دو عددی',
    'چراغ جلو خودرو کروز پلاس مدل 501 مناسب برای پژو 207 بسته دو عددی',
    'چراغ جلو خودرو گروه',
    'پژوهش صنعت مدرن مدل 02 مناسب برای پژو 207 بسته دو عددی',
    'چراغ جلو چپ کروز مدل 401 مناسب برای پژو 207',
    'چراغ جلو راست کروز مدل 501 مناسب برای پژو 207',
    'ست شیرآلات سیتکو مدل 207 مجموعه 4 عددی',
    'گردنبند طلا 18 عیار زنانه لیردا مدل فخری کد akm 207',
    'گردنبند طلا 18 عیار دخترانه لیردا مدل اسم فخری کد akm 207',
    'چراغ جلو کروز مدل 02 مناسب برای پژو 207',
    'کمک فنر جلو و عقب خودرو مدل SAHA مناسب برای پژو 207 بسته 4 عددی',
    'چراغ خطر عقب کروز مدل 01 مناسب برای پژو 206/207 بسته 2 عددی',
    'چراغ عقب کروز پلاس مدل 101-102مناسب برای پژو 206/207 بسته 2 عددی',
    'چراغ عقب کروز پلاس مدل 101-102مناسب برای پژو 206/207 بسته 2 عددی',
    'تیغه ابزار همه کاره فاین کد 207 بسته 2 عددی',
    'پخش کننده تصویری خودرو اینفینیتی مدل A10 مناسب برای پژو 207',
    'پخش کننده تصویری خودرو اینفینیتی کد N مناسب برای پژو 207',
  ]
})

const postResources = reactive({
  en: [
    "Manta Network Airdrop » Claim Free MANTA Tokens",
    "Fighting back: Turning the Tables on Web Scrapers Using Rust",
    "Devin AI vs Microsoft AutoDev, Who will eat your job first?",
    "A Practitioners Guide to Retrieval Augmented Generation (RAG)",
    "13 Docker Tricks You Didn’t Know",
    "Manta Network Airdrop » Claim Free MANTA Tokens",
    "Fighting back: Turning the Tables on Web Scrapers Using Rust",
    "Devin AI vs Microsoft AutoDev, Who will eat your job first?",
    "A Practitioners Guide to Retrieval Augmented Generation (RAG)",
    "13 Docker Tricks You Didn’t Know",
    "Create Mixtures of Experts with MergeKit",
    "You’re Decent At Python If You Can Answer These 7 Questions Correctly",
    "How to ace your engineering interview",
    "A Pinterest Engineering guide to technical interviews",
    "How to Crack System Design Interviews in 2024? Preparation Tips, Questions and Resources",
    "Career Switcher’s Guide to Your Dream Tech Job, Part 1",
    "Stories to Help You Grow as a Software Developer",
    "Manta Network Airdrop » Claim free MANTA tokens",
    "How past product experiences shape your UX",
    "I Went on the Dark Web and Instantly Regretted It",
    "Manta Network — Potential Airdrop Free Guide",
    "Nvidia, AI, and graphics hardware",
    "Manta Network Airdrop » Claim free MANTA tokens",
    "How past product experiences shape your UX",
    "I Went on the Dark Web and Instantly Regretted It",
    "Manta Network — Potential Airdrop Free Guide",
    "Nvidia, AI, and graphics hardware",
    "Insanity in the Air: The crash of Pakistan International Airlines flight 8303",
    "ALT staking goes LIVE, kicking off a multi-phased MACH Alpha launch",
    "Think, Then Speak: How Researchers Gave AI an Inner Monologue",
    "What I Learned as a Product Designer at Apple",
    "The Making of Apple’s Emoji: How designing these tiny icons changed my life",
    "Generative AI Recommended Reading",
    "My keynote talk for Medium Pub Crawl",
    "Reading Books Is Useless: Here’s a Better Way to Read",
    "$KWIF: The Cronos Chain Meerkat You Can’t Meer-gnore",
    "LinkedIn Just Banned Me Permanently Without a Reason (& It Makes Me Concerned About the Fragile…",
    "My keynote talk for Medium Pub Crawl",
    "Reading Books Is Useless: Here’s a Better Way to Read",
    "$KWIF: The Cronos Chain Meerkat You Can’t Meer-gnore",
    "LinkedIn Just Banned Me Permanently Without a Reason (& It Makes Me Concerned About the Fragile…",
    "Sometimes You Need To Delete That Article",
    "I Analyzed Every Major Writing Platform. These Are the Best Ones.",
    "Our favorite writing prompts and inspiration",
    "the secret ingredient to telling a good story",
    "I Tried 10 Extreme Creativity Hacks",
    "52 Writing Prompts to Inspire Your Next Blog Post",
    "My Favorite Writing Advice & Inspo",
    "Our favorite writing prompts and inspiration",
    "Stories To Help You Overcome Writer's Block",
    "Best of The Writing Cooperative",
  ],
  fa: [
    "ویزای استارتاپ از رویا تا واقعیت",
    "    کریپتوزواسپرمی: علل احتمالی تعداد بسیار کم اسپرم",
    "تست ایده استارتاپ | روش‌های تست ایده",
    "ویزیسان: مرجع علمی بیماری های پوستی مبتنی بر هوش مصنوعی",
    "به چرایی کسب و کار خود فکر کرده اید؟",
    "راهنمای کامل ایده‌پردازی برای کسب و کار اینترنتی: از ابتدا تا تحقق ایده",
    "کاهش بهره وری جهانی یائسگی! یک زیان 150 میلیارد دلاری",
    "رازهای پنهان جذب سرمایه در استارتاپ‌ها: 5 راز برای جلب سرمایه",
    "شاخصه‌های منابع انسانی و مسؤل استخدام حرفه‌ای در روند مصاحبه",
    "فاجعه‌ای به نام کارآفرینی در فضای دیجیتال ایران!",
    "با برون سپاری فرایند‌های کسب‌وکار، کسب‌وکار خودتون رو رشد بدین.",
    "چگونه تصمیم بگیریم که هرگز پشیمان نشویم؟",
    "آزمایش خون در آینده نزدیک چگونه خواهد بود؟",
    "گیت امنیتی فروشگاه: چرا، چگونه و چه نوعی؟",
    "روند تأمین مالی استارتاپ‌ها در سال 2024 که شما را در یک لحظه متعجب خواهد کرد",
    "چطوری زیرساخت موری رو با تیم فنی کوچیک مدیریت کردیم؟!",
    "۱۰ سریال مفید در حوزه کارآفرینی و استارتاپ",
    "همکاری در پروژه پرداخت یار و درگاه پرداخت",
    "ایده استارتاپی جدید برای هوش مصنوعی",
    "ساده ترین روش برای درست کردن یک پروداکت پلن",
    "لیست استارتاپ های تیم مهرداد و روش های همکاری",
    "راهنمای شروع به کار با استارتاپ: فراتر از روال زمانی",
    "چطوری یک فایل کامل برای معرفی کسب و کار خودتون درست کنید",
    "فرایند اخراج کارکنان و پایان دادن به همکاری",
    "چطوری برای کسب و کار خودمون یک برنامه مالی یک ساله داشته باشیم",
    "سه ویژگی اصلی برای دانش بنیان شدن یک شرکت",
    "راهکار در شهر هوشمند: بررسی مفهوم استارتاپ و سرمایه‌گذاری",
    "تفاوت دنیای استارتاپ و اختراعات همراه با طرح ده سوال شخصی",
    "بریم سمت معماری مایکروسرویس یا نه؟!",
    "چکیده‌ای از مقاله فین تک در ایران",
    "مسیر تبدیل شدن به یک رهبر خدمتگذار",
    "ایده استارتاپی ناب به نام پین استار",
    "معرفی 10 ایده استارتاپی خارجی برای بومی سازی در ایران",
    "چطور مدیر و رهبری بزرگوار و مهربان باشیم؟!",
    "فهم من از استارتاپ و چطور ساختنش",
    "استارتاپ چیست؟ و نحوه کار آن چگونه است؟",
    "کسب مقام دوم مسابقات ماراتن برنامه نویسی تلفن همراه MPM",
    "جوش‌های بلوغ کسب و کار (روش TRL)",
    "مدیریت پروژه آنلاین، ابزار دورکاری و مدیریت کسب‌وکار",
    "Stack Overflow Tour | ترجمه فارسی مقاله",
    "بدون دردسر برای سایتت یک درگاه پرداخت تهیه کن!",
    "تست نویسی در لاراول یا اسپرینگ بوت جاوا",
    "شیرجه عمیق به قلب Closure در جاواسکریپت",
    "راهنمای استفاده درست از چت بات های هوش مصنوعی مانند chat GPT پارت اول",
    "نصب برنامه اندروید در ویندوز 11",
    "مختصری از مهندسیِ نرم‌افزهایِ روش اجزاءِ محدود: ماتریس خلوت (sparse)",
    "مدیریت تنظیمات در پایتون و جنگو (Django)",
    "الگوریتم پیدا کردن کوتاه ترین مسیر در گراف غیر هم وزن",
    "لاراول ۱۱ - خلاصه کنفرانس ۲۰۲۴ (قسمت اول)",
    "خواندن فایل در Node.js با استفاده از ماژول‌های داخلی !!!",
    "تفاوت بین Application Class و Singleton چیست؟",
    "آموزش کامل Hoisting در جاوااسکریپت",
    "بنویسم یا ببینم؟ آموزش یا انجام؟",
    "چطور یک الگوریتم مسیریابی بنویسیم؟",
    "اگر یک برنامه نویس تازه کار هستید لطفا مطالعه کنید",
    "تعطیلات عید و یادگیری برنامه نویسی",
    "دریافت سفارش پروژه برنامه نویسی , هوشمند سازی, نرم افزاری, مارکتینگ",
    "راهنمای جامع اسناد نرم‌افزار: اطمینان از وضوح، قابلیت نگهداری و موفقیت",
    "معرفی PaL (بررسی تنظیمات php و لاراول)",
    "اندر احوالات جاوااسکریپت (قسمت چهارم)",
    "جدول هش یا Hash table چیست و چه کاربرد هایی دارد؟",
    "دل نوشته :: کار :: رشته کامپیوتر",
    "Developer Experience معیاری که نادیده گرفته شد",
    "امنیت ملی به زبان برنامه‌نویسی مرتبط است!",
    "چگونه برای پروژه های توسعه یافته تست بنویسیم؟",
    "باگ چیست؟ روش‌های رفع باگ به‌زبانی ساده برای برنامه‌نویسان",
    "کدومو انتخاب کنم؟ گیت هاب یا گیت لب؟!",
    "پایتون محبوب ترین زبان برنامه نویسی جهان",
    "اینترنت چی هست و چطوری کار میکنه ؟",
    "تجربه‌هایی ارزشمند در توسعه نرم‌افزار",
    "ویژگی Collection Expressions در سی شارپ 12",
    "استراتژی تقسیم و حل، چه کمکی در طراحی الگوریتم میکند؟",
  ]
})


const generateText = computed(() => {
  const lang = inputs.lang;
  const type = inputs.type


  if (type === 'paragraph') {
    let resource = JSON.stringify(wordResources[lang])
    resource = JSON.parse(resource)
    let output = []

    for (let i = 0; i < inputs.n; i++) {
      const p = generateSentences(resource, 3, inputs.isUnintelligible, lang, true)
      output.push(p)
    }

    return printResult(output, inputs.isTrainy)
  }
  if (type === 'sentence') {
    let resource = JSON.stringify(wordResources[lang])
    resource = JSON.parse(resource)

    return generateSentences(resource, inputs.n, inputs.isUnintelligible, lang, inputs.isTrainy)
  }
  if (type === 'word') {
    let resource = JSON.stringify(wordResources[lang])
    resource = JSON.parse(resource)

    let words = shuffleArray(removePunctuation(resource.join(' ')).split(' '))
    words = filterWordsByLength(words)
    words = words.splice(0, inputs.n)

    return printResult(words, inputs.isTrainy)
  }

  if (type === 'product') {
    return simpleResource(productResources[lang])
  }

  if (type === 'post') {
    return simpleResource(postResources[lang])
  }

  return printResult([], inputs.isTrainy)
})

function generateSentences(resource, n, isUnintelligible, lang, isTrainy) {
  let output = null
  let sentences = JSON.stringify(shuffleArray(resource))
  sentences = JSON.parse(sentences)
  sentences = sentences.splice(0, n)

  if (isUnintelligible) {
    let newSentences = []

    sentences.forEach(sentence => {
      let newSentence = shuffleArray(removePunctuation(sentence).split(' ')).join(' ') + pickRandomItem(getPunctuations(lang))
      newSentence = newSentence.toLowerCase()
      newSentence = toSentenceCase(newSentence)

      newSentences.push(newSentence)
    })

    output = newSentences
  } else {
    output = sentences
  }

  return printResult(output, isTrainy)
}

function removePunctuation(str) {
  var regex = /[!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~]/g;
  return str.replace(regex, '');
}

function shuffleArray(array) {
  // Loop through the array in reverse order
  for (let i = array.length - 1; i > 0; i--) {
    // Generate a random index from 0 to i
    const j = Math.floor(Math.random() * (i + 1));
    // Swap array[i] and array[j]
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}

function pickRandomItem(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}

function toSentenceCase(str) {
  // Convert the first character to uppercase and the rest to lowercase
  // Preserving the capitalization for the word "I"
  return str.replace(/(^|\. *)([a-z])/g, function (match, separator, char) {
    return separator + char.toUpperCase();
  });
}

function filterWordsByLength(strings) {
  // Initialize an empty array to store the filtered words
  let filteredWords = [];

  // Loop through each string in the input list
  strings.forEach(function (str) {
    // Split the string into words
    let words = str.split(" ");

    // Filter out the words with length greater than 3 characters
    let longWords = words.filter(function (word) {
      return word.length > 3;
    });

    // Concatenate the filtered words to the result array
    filteredWords = filteredWords.concat(longWords);
  });

  // Return the filtered words array
  return filteredWords;
}

function printResult(array, isTrainy) {
  let output = ''
  if (isTrainy) {
    return (array.join(' '))
  } else {
    array.forEach(item => {
      output += "<p>" + item + "</p>"
    })
    return output
  }
}

function getPunctuations(lang) {
  if (lang === 'fa' || lang === 'azb' || lang === 'ar') {
    return ['.', '!', '؟']
  } else {
    return ['.', '!', '?']
  }
}

function simpleResource(input) {
  let resource = JSON.stringify(input)
  resource = JSON.parse(resource)
  let items = shuffleArray(resource)
  items = items.splice(0, inputs.n)

  return printResult(items, false)
}

</script>

<template>

  <div class="container py-5">
    <div class="row justify-content-center gy-5 gx-sm-5">
      <div class="col-lg-3">
        <h1 class="mb-4">
          <img class="logo" src="./assets/logo.svg" alt="ابزار تولید کننده متن لورم ایپسوم">
        </h1>
        <p class="mb-4">
          با استفاده از این ابزار متن‌های لورم ایپسوم با تنوع بالا تولید کنید. ویژگی‌های مختلف و زبان‌های مختلف را تنظیم کنید تا متن لورم ایپسوم منحصر به فرد خود را ایجاد کنید.
        </p>

        <div class="d-flex flex-wrap gap-2">
          <a href="https://github.com/ormanfaghihi/lorem-ipsum-generator" target="_blank" class="btn btn-sm btn-dark">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-github me-2" viewBox="0 0 16 16">
              <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27s1.36.09 2 .27c1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.01 8.01 0 0 0 16 8c0-4.42-3.58-8-8-8">

              </path>
            </svg>
            لینک پروژه در گیتهاب
          </a>
          <a rel="follow" href="https://l00p.dev/" class="btn btn-sm btn-primary"> لووپ استودیو </a>
        </div>
      </div>
      <div class="col-lg-6">
        <div class="controls mb-4">
          <div class="row g-3">

            <div class="col-12 col-sm-4">
              <select class="form-select" v-model="inputs.type">
                <option value="paragraph">پاراگراف</option>
                <option value="sentence">جمله</option>
                <option value="word">کلمه</option>
                <option value="product">عنوان محصول</option>
                <option value="post">عنوان پست وبلاگ</option>
                <!--        <option value="name">نام فرد</option>-->
                <!--        <option value="comment">کامنت</option>-->
              </select>
            </div>
            <div class="col-12 col-sm-4">
              <select class="form-select" v-model="inputs.lang">
                <option value="en">انگلیسی</option>
                <option value="fa">فارسی</option>

                <!--        <option value="tr">Türkçe</option>-->
                <!--        <option value="az">Azərbaycanca</option>-->
                <!--        <option value="azb">تۆرکجه</option>-->
                <!--        <option value="ar">العربية</option>-->
              </select>
            </div>
            <div class="col-12 col-sm-4">
              <div class="d-flex gap-2 align-items-center">
                <input v-model="inputs.n" value="10" class="form-control text-center" readonly>

                <div class="btn-group">
                  <button type="button" class="btn btn-outline-primary" @click="inputs.n ++">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-lg" viewBox="0 0 16 16">
                      <path fill-rule="evenodd" d="M8 2a.5.5 0 0 1 .5.5v5h5a.5.5 0 0 1 0 1h-5v5a.5.5 0 0 1-1 0v-5h-5a.5.5 0 0 1 0-1h5v-5A.5.5 0 0 1 8 2"></path>
                    </svg>
                  </button>
                  <button type="button" class="btn btn-outline-primary" @click="inputs.n --" :disabled="inputs.n <= 1">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-dash-lg" viewBox="0 0 16 16">
                      <path fill-rule="evenodd" d="M2 8a.5.5 0 0 1 .5-.5h11a.5.5 0 0 1 0 1h-11A.5.5 0 0 1 2 8"/>
                    </svg>
                  </button>
                </div>

              </div>

            </div>

            <div class="col-12 d-flex flex-wrap gap-4" v-if="inputs.type === 'paragraph' || inputs.type === 'sentence' || inputs.type ===  'word'">
              <label class="form-check" v-if="inputs.type === 'paragraph' || inputs.type === 'sentence' || inputs.type ===  'word'">
                <input class="form-check-input" type="checkbox" v-model="inputs.isTrainy">
                <div class="form-check-label">
                  عبارات پشت سر هم باشند.
                </div>
              </label>

              <label class="form-check" v-if="inputs.type === 'paragraph' || inputs.type === 'sentence'">
                <input class="form-check-input" type="checkbox" v-model="inputs.isUnintelligible">
                <div class="form-check-label">
                  عبارات نامفهوم باشند؟
                </div>
              </label>
            </div>

          </div>
        </div>

        <div class="output" :dir="inputs.lang==='en' ? 'ltr' : 'rtl'" v-html="generateText"></div>
      </div>
    </div>
  </div>


</template>


<style>
* {
  font-family: Vazirmatn;
}

.logo {
  max-width: 250px;
}

body {
  font-size: 16px;
  line-height: 1.6;
  background-color: #d0d6dc;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='40' height='40' viewBox='0 0 40 40'%3E%3Cg fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.4'%3E%3Cpath d='M0 38.59l2.83-2.83 1.41 1.41L1.41 40H0v-1.41zM0 1.4l2.83 2.83 1.41-1.41L1.41 0H0v1.41zM38.59 40l-2.83-2.83 1.41-1.41L40 38.59V40h-1.41zM40 1.41l-2.83 2.83-1.41-1.41L38.59 0H40v1.41zM20 18.6l2.83-2.83 1.41 1.41L21.41 20l2.83 2.83-1.41 1.41L20 21.41l-2.83 2.83-1.41-1.41L18.59 20l-2.83-2.83 1.41-1.41L20 18.59z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}

.output {
  background-color: white;
  padding: 32px;
  border-radius: 10px;
  box-shadow: 0 8px 12px rgba(0,0,0,0.15);
  background-color: #2e3c4d;
  color: white;
  background-image: url("data:image/svg+xml,%3Csvg width='52' height='26' viewBox='0 0 52 26' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.08'%3E%3Cpath d='M10 10c0-2.21-1.79-4-4-4-3.314 0-6-2.686-6-6h2c0 2.21 1.79 4 4 4 3.314 0 6 2.686 6 6 0 2.21 1.79 4 4 4 3.314 0 6 2.686 6 6 0 2.21 1.79 4 4 4v2c-3.314 0-6-2.686-6-6 0-2.21-1.79-4-4-4-3.314 0-6-2.686-6-6zm25.464-1.95l8.486 8.486-1.414 1.414-8.486-8.486 1.414-1.414z' /%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}

.controls {
  background-color: white;
  padding: 32px;
  border-radius: 10px;
  box-shadow: 0 8px 12px rgba(0,0,0,0.15);
  position: sticky;
  top: 0;
  transform-origin: top center;
  //transform: scale(1.03);

}

.controls::after {
  content: "";
  background-color: rgba(255,255,255, 0.2);
  position: absolute;
  z-index: -1;
  left: 50%;
  transform: translateX(-50%);
  top: 100%;
  width: 85%;
  height: 12px;
  border-radius:  0 0 10px 10px;
  backdrop-filter: blur(10px);
}

.output p {
  margin-bottom: 18px;
}
.output p:last-child {
  margin-bottom: 0;
}
</style>


