test code"use client";

import { useState, useEffect } from "react";
import Link from "next/link";
import { Moon, Sun, CheckCircle, Shield, BarChart3, Zap, MessageCircle, Clock } from "lucide-react";

// Platform icons as components
const TikTokIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="currentColor">
    <path d="M19.59 6.69a4.83 4.83 0 0 1-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 0 1-5.2 1.74 2.89 2.89 0 0 1 2.31-4.64 2.93 2.93 0 0 1 .88.13V9.4a6.84 6.84 0 0 0-1-.05A6.33 6.33 0 0 0 5 20.1a6.34 6.34 0 0 0 10.86-4.43v-7a8.16 8.16 0 0 0 4.77 1.52v-3.4a4.85 4.85 0 0 1-1-.1z"/>
  </svg>
);

const InstagramIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <rect width="20" height="20" x="2" y="2" rx="5" ry="5"/>
    <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/>
    <line x1="17.5" x2="17.51" y1="6.5" y2="6.5"/>
  </svg>
);

const YouTubeIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="currentColor">
    <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
  </svg>
);

const SpotifyIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="currentColor">
    <path d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.54.78.241 1.2zm.12-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"/>
  </svg>
);

const FacebookIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="currentColor">
    <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
  </svg>
);

const RedditIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="currentColor">
    <path d="M12 0A12 12 0 0 0 0 12a12 12 0 0 0 12 12 12 12 0 0 0 12-12A12 12 0 0 0 12 0zm5.01 4.744c.688 0 1.25.561 1.25 1.249a1.25 1.25 0 0 1-2.498.056l-2.597-.547-.8 3.747c1.824.07 3.48.632 4.674 1.488.308-.309.73-.491 1.207-.491.968 0 1.754.786 1.754 1.754 0 .716-.435 1.333-1.01 1.614a3.111 3.111 0 0 1 .042.52c0 2.694-3.13 4.87-7.004 4.87-3.874 0-7.004-2.176-7.004-4.87 0-.183.015-.366.043-.534A1.748 1.748 0 0 1 4.028 12c0-.968.786-1.754 1.754-1.754.463 0 .898.196 1.207.49 1.207-.883 2.878-1.43 4.744-1.487l.885-4.182a.342.342 0 0 1 .14-.197.35.35 0 0 1 .238-.042l2.906.617a1.214 1.214 0 0 1 1.108-.701zM9.25 12C8.561 12 8 12.562 8 13.25c0 .687.561 1.248 1.25 1.248.687 0 1.248-.561 1.248-1.249 0-.688-.561-1.249-1.249-1.249zm5.5 0c-.687 0-1.248.561-1.248 1.25 0 .687.561 1.248 1.249 1.248.688 0 1.249-.561 1.249-1.249 0-.687-.562-1.249-1.25-1.249zm-5.466 3.99a.327.327 0 0 0-.231.094.33.33 0 0 0 0 .463c.842.842 2.484.913 2.961.913.477 0 2.105-.056 2.961-.913a.361.361 0 0 0 .029-.463.33.33 0 0 0-.464 0c-.547.533-1.684.73-2.512.73-.828 0-1.979-.196-2.512-.73a.326.326 0 0 0-.232-.095z"/>
  </svg>
);

const XIcon = ({ className }: { className?: string }) => (
  <svg className={className} viewBox="0 0 24 24" fill="currentColor">
    <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
  </svg>
);

const platforms = ["يوتيوب", "تيك توك", "إنستغرام", "فيسبوك", "سبوتيفاي"];
const platformColors: Record<string, string> = {
  "يوتيوب": "text-red-500",
  "تيك توك": "text-black dark:text-white",
  "إنستغرام": "text-pink-500",
  "فيسبوك": "text-blue-600",
  "سبوتيفاي": "text-green-500",
};

const platformIcons: Record<string, React.ReactNode> = {
  "يوتيوب": <YouTubeIcon className="w-6 h-6 inline-block mr-2 text-red-500" />,
  "تيك توك": <TikTokIcon className="w-6 h-6 inline-block mr-2" />,
  "إنستغرام": <InstagramIcon className="w-6 h-6 inline-block mr-2 text-pink-500" />,
  "فيسبوك": <FacebookIcon className="w-6 h-6 inline-block mr-2 text-blue-600" />,
  "سبوتيفاي": <SpotifyIcon className="w-6 h-6 inline-block mr-2 text-green-500" />,
};

const testimonials = [
  {
    quote: "لم أتوقع الكثير في البداية، لكن زيد فولو فاجأني. بدأت ألاحظ المزيد من النشاط على منشوراتي على الفور تقريباً، وشعرت أنه طبيعي وليس مزعجاً.",
    name: "سارة ك.",
    role: "مؤثرة",
  },
  {
    quote: "كنت أحاول تنمية حسابي لأشهر دون أي تقدم. بعد استخدام زيد فولو، بدأت أرى نتائج ثابتة. أشخاص حقيقيون يتفاعلون مع محتواي.",
    name: "جاي د.",
    role: "مدير علامة تجارية",
  },
  {
    quote: "كانت الدفعة خفيفة لكن ملحوظة - المزيد من التعليقات، المزيد من الحفظ، المزيد من الاهتمام العام. جعلني أشعر أن محتواي لم يعد يختفي في الفراغ.",
    name: "ليندا س.",
    role: "صانعة محتوى",
  },
  {
    quote: "حسابي كان عالقاً عند نفس المستوى للأبد. زيد فولو أعطاه تلك الشرارة الصغيرة لتحريك الأمور مرة أخرى. لوحة التحكم بسيطة ولا شيء مربك.",
    name: "ماركو ت.",
    role: "مسوق رقمي",
  },
  {
    quote: "أعمل مع العلامات التجارية بانتظام والبقاء مرئياً هو جزء أساسي من عملي. زيد فولو ساعدني في الحفاظ على نشاط الأمور عندما انخفض وصولي.",
    name: "كلوي ر.",
    role: "مدونة أسلوب حياة",
  },
  {
    quote: "ما أقدره أكثر هو أن النمو شعرت أنه عضوي. كان تدريجياً وقابلاً للتصديق. ساعدني حقاً في استعادة وصولي بعد أشهر من المعاناة.",
    name: "دانيال ف.",
    role: "صاحب مشروع صغير",
  },
];

const avatarGradients = [
  "from-pink-400 to-rose-500",
  "from-violet-400 to-purple-500",
  "from-blue-400 to-indigo-500",
  "from-emerald-400 to-teal-500",
  "from-amber-400 to-orange-500",
  "from-cyan-400 to-sky-500",
];

const avatarInitials = ["أح", "سم", "مر", "نو", "فا", "كر"];

export default function Home() {
  const [currentPlatform, setCurrentPlatform] = useState(0);
  const [isDark, setIsDark] = useState(false);

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentPlatform((prev) => (prev + 1) % platforms.length);
    }, 2000);
    return () => clearInterval(interval);
  }, []);

  useEffect(() => {
    if (isDark) {
      document.documentElement.classList.add("dark");
    } else {
      document.documentElement.classList.remove("dark");
    }
  }, [isDark]);

  return (
    <div className="min-h-screen bg-background">
      {/* Header */}
      <header className="sticky top-0 z-50 bg-background/80 backdrop-blur-md border-b border-border/50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex items-center justify-between h-16">
            {/* Logo */}
            <Link href="/" className="flex items-center space-x-2 space-x-reverse">
              <div className="w-8 h-8 rounded-full bg-gradient-to-br from-emerald-400 to-teal-500 flex items-center justify-center">
                <CheckCircle className="w-5 h-5 text-white" />
              </div>
              <span className="font-bold text-lg">زيد فولو</span>
            </Link>

            {/* Navigation */}
            <nav className="hidden md:flex items-center space-x-6 space-x-reverse">
              <Link href="#" className="flex items-center space-x-1.5 space-x-reverse text-sm text-muted-foreground hover:text-foreground transition-colors">
                <TikTokIcon className="w-4 h-4" />
                <span>تيك توك</span>
              </Link>
              <Link href="#" className="flex items-center space-x-1.5 space-x-reverse text-sm text-muted-foreground hover:text-foreground transition-colors">
                <InstagramIcon className="w-4 h-4" />
                <span>إنستغرام</span>
              </Link>
              <Link href="#" className="flex items-center space-x-1.5 space-x-reverse text-sm text-muted-foreground hover:text-foreground transition-colors">
                <YouTubeIcon className="w-4 h-4" />
                <span>يوتيوب</span>
              </Link>
              <Link href="#" className="flex items-center space-x-1.5 space-x-reverse text-sm text-muted-foreground hover:text-foreground transition-colors">
                <FacebookIcon className="w-4 h-4" />
                <span>فيسبوك</span>
              </Link>
              <Link href="#" className="flex items-center space-x-1.5 space-x-reverse text-sm text-muted-foreground hover:text-foreground transition-colors">
                <SpotifyIcon className="w-4 h-4" />
                <span>سبوتيفاي</span>
              </Link>
              <Link href="#" className="flex items-center space-x-1.5 space-x-reverse text-sm text-muted-foreground hover:text-foreground transition-colors">
                <XIcon className="w-4 h-4" />
                <span>إكس</span>
              </Link>
            </nav>

            {/* Right side */}
            <div className="flex items-center space-x-4 space-x-reverse">
              <Link href="#" className="text-sm text-muted-foreground hover:text-foreground transition-colors">
                تواصل معنا
              </Link>
              <button
                onClick={() => setIsDark(!isDark)}
                className="p-2 rounded-full hover:bg-muted transition-colors"
              >
                {isDark ? <Sun className="w-5 h-5" /> : <Moon className="w-5 h-5" />}
              </button>
            </div>
          </div>
        </div>
      </header>

      {/* Hero Section */}
      <section className="relative overflow-hidden">
        {/* Background gradient */}
        <div className="absolute inset-0 bg-gradient-to-br from-blue-50 via-purple-50/30 to-pink-50/20 dark:from-blue-950/20 dark:via-purple-950/10 dark:to-pink-950/10" />

        <div className="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20 text-center">
          <h1 className="text-4xl md:text-5xl lg:text-6xl font-bold tracking-tight mb-6">
            نمِّ حسابك على
            <span className={`transition-colors duration-300 ${platformColors[platforms[currentPlatform]]}`}>
              {" "}{platforms[currentPlatform]}
            </span>
            {platformIcons[platforms[currentPlatform]]}
          </h1>

          <p className="text-lg text-muted-foreground max-w-2xl mx-auto mb-8">
            نُدير <span className="font-semibold text-foreground">حملات إعلانية مدفوعة</span> على إعلانات تيك توك وميتا
            وجوجل والمزيد للترويج لحسابك
          </p>

          {/* Avatars */}
          <div className="flex justify-center -space-x-3 space-x-reverse mb-16">
            {avatarGradients.map((gradient, i) => (
              <div
                key={i}
                className={`w-12 h-12 rounded-full border-2 border-white dark:border-gray-800 shadow-md bg-gradient-to-br ${gradient} flex items-center justify-center text-white font-semibold text-sm`}
              >
                {avatarInitials[i]}
              </div>
            ))}
          </div>

          {/* Choose Your Platform */}
          <div className="mt-16">
            <h2 className="text-3xl md:text-4xl font-bold mb-4">اختر منصتك</h2>
            <p className="text-muted-foreground mb-10">
              حدد منصة التواصل الاجتماعي التي تريد تنميتها واطلب حملة مخصصة.
            </p>

            <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 max-w-5xl mx-auto">
              {/* TikTok Card */}
              <div className="bg-card rounded-2xl p-6 shadow-sm border border-border hover:shadow-lg hover:border-emerald-200 transition-all group">
                <TikTokIcon className="w-10 h-10 mx-auto mb-4" />
                <h3 className="font-bold text-lg mb-2">تيك توك</h3>
                <p className="text-sm text-muted-foreground mb-4">
                  عزز حضورك على تيك توك باستراتيجيات المحتوى الفيروسي وأدوات النمو.
                </p>
                <button className="w-full py-2.5 px-4 bg-emerald-500 hover:bg-emerald-600 text-white rounded-full text-sm font-medium transition-colors">
                  ابدأ الآن
                </button>
              </div>

              {/* Instagram Card */}
              <div className="bg-card rounded-2xl p-6 shadow-sm border border-border hover:shadow-lg hover:border-pink-200 transition-all group">
                <InstagramIcon className="w-10 h-10 mx-auto mb-4 text-pink-500" />
                <h3 className="font-bold text-lg mb-2">إنستغرام</h3>
                <p className="text-sm text-muted-foreground mb-4">
                  نمِّ جمهورك على إنستغرام بحملات مستهدفة ووصول حقيقي.
                </p>
                <button className="w-full py-2.5 px-4 bg-emerald-500 hover:bg-emerald-600 text-white rounded-full text-sm font-medium transition-colors">
                  ابدأ الآن
                </button>
              </div>

              {/* YouTube Card */}
              <div className="bg-card rounded-2xl p-6 shadow-sm border border-border hover:shadow-lg hover:border-red-200 transition-all group">
                <YouTubeIcon className="w-10 h-10 mx-auto mb-4 text-red-500" />
                <h3 className="font-bold text-lg mb-2">يوتيوب</h3>
                <p className="text-sm text-muted-foreground mb-4">
                  وسّع قناتك على يوتيوب باستراتيجيات نمو الجمهور المثبتة.
                </p>
                <button className="w-full py-2.5 px-4 bg-emerald-500 hover:bg-emerald-600 text-white rounded-full text-sm font-medium transition-colors">
                  ابدأ الآن
                </button>
              </div>

              {/* Facebook Card */}
              <div className="bg-card rounded-2xl p-6 shadow-sm border border-border hover:shadow-lg hover:border-blue-200 transition-all group">
                <FacebookIcon className="w-10 h-10 mx-auto mb-4 text-blue-600" />
                <h3 className="font-bold text-lg mb-2">فيسبوك</h3>
                <p className="text-sm text-muted-foreground mb-4">
                  زِد متابعي صفحتك على فيسبوك بحملات ترويجية احترافية ومستهدفة.
                </p>
                <button className="w-full py-2.5 px-4 bg-emerald-500 hover:bg-emerald-600 text-white rounded-full text-sm font-medium transition-colors">
                  ابدأ الآن
                </button>
              </div>

              {/* Spotify Card */}
              <div className="bg-card rounded-2xl p-6 shadow-sm border border-border hover:shadow-lg hover:border-green-200 transition-all group">
                <SpotifyIcon className="w-10 h-10 mx-auto mb-4 text-green-500" />
                <h3 className="font-bold text-lg mb-2">سبوتيفاي</h3>
                <p className="text-sm text-muted-foreground mb-4">
                  نمِّ حضورك على سبوتيفاي بترويج مميز وتوسيع الجمهور.
                </p>
                <button className="w-full py-2.5 px-4 bg-emerald-500 hover:bg-emerald-600 text-white rounded-full text-sm font-medium transition-colors">
                  ابدأ الآن
                </button>
              </div>

              {/* X Card */}
              <div className="bg-card rounded-2xl p-6 shadow-sm border border-border hover:shadow-lg hover:border-gray-300 transition-all group">
                <XIcon className="w-10 h-10 mx-auto mb-4" />
                <h3 className="font-bold text-lg mb-2">إكس (تويتر)</h3>
                <p className="text-sm text-muted-foreground mb-4">
                  نمِّ حضورك على إكس بترويج مستهدف وتوسيع الجمهور.
                </p>
                <button className="w-full py-2.5 px-4 bg-emerald-500 hover:bg-emerald-600 text-white rounded-full text-sm font-medium transition-colors">
                  ابدأ الآن
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Our Promotion Method */}
      <section className="py-20 bg-background">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <span className="inline-flex items-center px-4 py-2 rounded-full bg-emerald-50 dark:bg-emerald-950/30 text-emerald-600 dark:text-emerald-400 text-sm font-medium mb-6">
            <Zap className="w-4 h-4 ml-2" />
            طريقة الترويج لدينا
          </span>

          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            نشتري إعلانات للترويج لحسابك
          </h2>
          <p className="text-muted-foreground max-w-2xl mx-auto mb-12">
            طريقتنا بسيطة وشفافة تماماً: نقوم بإنشاء وتشغيل{" "}
            <span className="font-semibold text-foreground">حملات إعلانية مدفوعة</span> على المنصات الرئيسية لجلب مستخدمين حقيقيين إلى حسابك.
          </p>

          {/* Ad Platforms */}
          <div className="flex flex-wrap justify-center gap-4 mb-16">
            {[
              { name: "إعلانات تيك توك", icon: <TikTokIcon className="w-8 h-8" /> },
              { name: "إعلانات ميتا", icon: <FacebookIcon className="w-8 h-8 text-blue-600" /> },
              { name: "إعلانات جوجل", icon: <svg className="w-8 h-8" viewBox="0 0 24 24" fill="currentColor"><path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/><path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/><path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/><path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/></svg> },
              { name: "إعلانات يوتيوب", icon: <YouTubeIcon className="w-8 h-8 text-red-500" /> },
              { name: "إعلانات إنستغرام", icon: <InstagramIcon className="w-8 h-8 text-pink-500" /> },
              { name: "إعلانات فيسبوك", icon: <FacebookIcon className="w-8 h-8 text-blue-600" /> },
            ].map((platform) => (
              <div
                key={platform.name}
                className="flex flex-col items-center justify-center w-28 h-24 bg-muted/50 rounded-xl hover:bg-muted transition-colors"
              >
                {platform.icon}
                <span className="text-xs mt-2 text-muted-foreground">{platform.name}</span>
              </div>
            ))}
          </div>

          {/* How It Works */}
          <h3 className="text-2xl font-bold mb-10">كيف يعمل</h3>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 max-w-5xl mx-auto">
            {[
              {
                step: 1,
                title: "تختار باقة",
                description: "حدد منصتك المستهدفة وباقة النمو بناءً على أهدافك وميزانيتك.",
                icon: <svg className="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" /></svg>,
              },
              {
                step: 2,
                title: "نُنشئ حملات إعلانية",
                description: "فريقنا يصمم ويطلق حملات إعلانية مدفوعة على منصات الإعلانات الرئيسية للترويج لحسابك.",
                icon: <svg className="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z" /></svg>,
              },
              {
                step: 3,
                title: "وصول جمهور مستهدف",
                description: "يُعرض حسابك لمستخدمين حقيقيين من خلال إعلانات مدفوعة شرعية، مستهدفة حسب الاهتمامات والديموغرافيا.",
                icon: <svg className="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" /></svg>,
              },
              {
                step: 4,
                title: "تحصل على نمو حقيقي",
                description: "المستخدمون الذين يرون إعلاناتنا ويهتمون بمحتواك سيكتشفون ويتفاعلون مع حسابك.",
                icon: <svg className="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={1.5} d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" /></svg>,
              },
            ].map((item) => (
              <div
                key={item.step}
                className="relative bg-gradient-to-br from-emerald-50/50 to-teal-50/30 dark:from-emerald-950/20 dark:to-teal-950/10 rounded-2xl p-6 text-center"
              >
                <span className="absolute -top-3 left-1/2 -translate-x-1/2 w-7 h-7 bg-emerald-500 text-white text-sm font-bold rounded-full flex items-center justify-center">
                  {item.step}
                </span>
                <div className="w-14 h-14 mx-auto mb-4 rounded-xl bg-white dark:bg-gray-800 shadow-sm flex items-center justify-center text-emerald-600">
                  {item.icon}
                </div>
                <h4 className="font-bold mb-2">{item.title}</h4>
                <p className="text-sm text-muted-foreground">{item.description}</p>
              </div>
            ))}
          </div>

          {/* Compliance badges */}
          <div className="mt-12 bg-muted/30 rounded-2xl p-6 max-w-3xl mx-auto">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
              <div className="flex items-start space-x-3 space-x-reverse">
                <Shield className="w-6 h-6 text-emerald-500 flex-shrink-0" />
                <div className="text-right">
                  <h4 className="font-bold">متوافق 100%</h4>
                  <p className="text-sm text-muted-foreground">جميع الحملات تتبع سياسات إعلانات المنصات وشروط الخدمة.</p>
                </div>
              </div>
              <div className="flex items-start space-x-3 space-x-reverse">
                <BarChart3 className="w-6 h-6 text-emerald-500 flex-shrink-0" />
                <div className="text-right">
                  <h4 className="font-bold">طريقة شفافة</h4>
                  <p className="text-sm text-muted-foreground">نستخدم نفس أساليب الإعلان المدفوع التي تستخدمها العلامات التجارية والوكالات الكبرى حول العالم.</p>
                </div>
              </div>
            </div>
            <div className="border-t border-border pt-4">
              <p className="text-sm">
                <span className="text-emerald-500 font-medium">✓ إعلانات شرعية</span>
                <span className="text-muted-foreground"> — نستخدم نفس أساليب الترويج المدفوع مثل شركات Fortune 500 والوكالات الرقمية والمعلنين المعتمدين حول العالم.</span>
              </p>
            </div>
          </div>
        </div>
      </section>

      {/* Testimonials */}
      <section className="py-20 bg-muted/30 overflow-hidden">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <h2 className="text-3xl md:text-4xl font-bold text-center mb-12">ماذا يقول مستخدمونا</h2>

          <div className="relative">
            <div className="flex animate-scroll gap-6">
              {[...testimonials, ...testimonials].map((testimonial, i) => (
                <div
                  key={i}
                  className="flex-shrink-0 w-80 bg-card rounded-2xl p-6 shadow-sm border border-border"
                >
                  <p className="text-sm text-muted-foreground mb-4 italic">"{testimonial.quote}"</p>
                  <div>
                    <p className="font-semibold">{testimonial.name}</p>
                    <p className="text-xs text-muted-foreground">{testimonial.role}</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* Professional Services */}
      <section className="py-20 bg-background">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <h2 className="text-3xl md:text-4xl font-bold mb-4">خدمات إعلانية احترافية</h2>
          <p className="text-muted-foreground max-w-2xl mx-auto mb-12">
            انضم إلى أكثر من 25,000 صانع محتوى وعلامة تجارية نمّوا جمهورهم من خلال حملاتنا الإعلانية المدفوعة الشرعية.
          </p>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-4xl mx-auto">
            <div className="bg-card rounded-2xl p-6 shadow-sm border border-border">
              <div className="w-12 h-12 mx-auto mb-4 rounded-xl bg-emerald-100 dark:bg-emerald-900/30 flex items-center justify-center">
                <Shield className="w-6 h-6 text-emerald-600" />
              </div>
              <h3 className="font-bold mb-2">بدون وصول لحسابك</h3>
              <p className="text-sm text-muted-foreground">بيانات اعتمادك تبقى معك. نحتاج فقط رابطك العام للبدء.</p>
            </div>

            <div className="bg-card rounded-2xl p-6 shadow-sm border border-border">
              <div className="w-12 h-12 mx-auto mb-4 rounded-xl bg-emerald-100 dark:bg-emerald-900/30 flex items-center justify-center">
                <Clock className="w-6 h-6 text-emerald-600" />
              </div>
              <h3 className="font-bold mb-2">تحديثات مباشرة للطلب</h3>
              <p className="text-sm text-muted-foreground">شاهد حملتك تتطور مع تحديثات التقدم الفورية على لوحة التحكم.</p>
            </div>

            <div className="bg-card rounded-2xl p-6 shadow-sm border border-border">
              <div className="w-12 h-12 mx-auto mb-4 rounded-xl bg-emerald-100 dark:bg-emerald-900/30 flex items-center justify-center">
                <MessageCircle className="w-6 h-6 text-emerald-600" />
              </div>
              <h3 className="font-bold mb-2">دعم على مدار الساعة</h3>
              <p className="text-sm text-muted-foreground">أشخاص حقيقيون، إجابات حقيقية، في أي وقت. فريقنا مكرس لنجاحك.</p>
            </div>
          </div>
        </div>
      </section>

      {/* Stats Section */}
      <section className="py-20 bg-gradient-to-br from-pink-100 via-purple-100 to-blue-100 dark:from-pink-950/30 dark:via-purple-950/30 dark:to-blue-950/30 animate-gradient">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <h2 className="text-3xl md:text-4xl font-bold mb-12">نمو حقيقي. أرقام حقيقية.</h2>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-4xl mx-auto">
            <div className="bg-white/60 dark:bg-gray-900/40 backdrop-blur-sm rounded-2xl p-8">
              <div className="text-5xl md:text-6xl font-bold bg-gradient-to-r from-pink-500 to-rose-500 bg-clip-text text-transparent">
                +100M
              </div>
              <p className="text-muted-foreground mt-2">تفاعلات تم توصيلها</p>
            </div>

            <div className="bg-white/60 dark:bg-gray-900/40 backdrop-blur-sm rounded-2xl p-8">
              <div className="text-5xl md:text-6xl font-bold bg-gradient-to-r from-orange-500 to-amber-500 bg-clip-text text-transparent">
                +4.9
              </div>
              <p className="text-muted-foreground mt-2">متوسط تقييم العملاء</p>
            </div>

            <div className="bg-white/60 dark:bg-gray-900/40 backdrop-blur-sm rounded-2xl p-8">
              <div className="text-5xl md:text-6xl font-bold bg-gradient-to-r from-teal-500 to-emerald-500 bg-clip-text text-transparent">
                78K+
              </div>
              <p className="text-muted-foreground mt-2">حملات مكتملة</p>
            </div>
          </div>
        </div>
      </section>

      {/* About Section */}
      <section className="py-20 bg-background">
        <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <h2 className="text-3xl md:text-4xl font-bold mb-8">وكالة إعلانية شرعية</h2>

          <div className="bg-muted/30 rounded-2xl p-8 text-right space-y-4">
            <p className="text-muted-foreground">
              زيد فولو هي <span className="font-semibold text-foreground">وكالة إعلانية مدفوعة</span> لصناع المحتوى والمؤثرين والعلامات التجارية المستعدين لتوسيع حضورهم الرقمي. نُنشئ ونُدير حملات إعلانية احترافية على المنصات الرئيسية لجلب جماهير حقيقية ومتفاعلة إلى حسابك.
            </p>
            <p className="text-muted-foreground">
              <span className="font-semibold text-foreground">طريقتنا بسيطة وشفافة:</span> نشتري مساحة إعلانية على منصات مثل إعلانات تيك توك وميتا (فيسبوك وإنستغرام) وجوجل ويوتيوب للترويج لمحتواك لجماهير مستهدفة. هذه هي نفس طريقة الإعلان الشرعية المستخدمة من قبل العلامات التجارية الكبرى حول العالم.
            </p>
            <p className="text-muted-foreground">
              كل حملة متوافقة تماماً مع سياسات إعلانات المنصات. نتولى العملية بأكملها — من إنشاء الإعلان إلى استهداف الجمهور إلى تحسين الحملة — حتى تتمكن من التركيز على إنشاء محتوى رائع بينما نقود النمو من خلال الترويج المدفوع.
            </p>
            <p className="font-semibold">
              نحن فريق متخصص من خبراء الإعلان الرقمي نساعدك على النمو من خلال حملات إعلانية مدفوعة شرعية وشفافة.
            </p>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-12 bg-background border-t border-border">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <div className="flex justify-center space-x-6 space-x-reverse mb-6">
            <Link href="#" className="text-sm text-muted-foreground hover:text-foreground transition-colors">
              شروط الخدمة
            </Link>
            <span className="text-muted-foreground">•</span>
            <Link href="#" className="text-sm text-muted-foreground hover:text-foreground transition-colors">
              سياسة الخصوصية
            </Link>
            <span className="text-muted-foreground">•</span>
            <Link href="#" className="text-sm text-muted-foreground hover:text-foreground transition-colors">
              سياسة الاسترداد
            </Link>
          </div>

          <p className="text-sm text-muted-foreground mb-4">
            حقوق النشر © 2025 ZidFollow.com
          </p>

          <p className="text-xs text-muted-foreground/70 max-w-2xl mx-auto">
            زيد فولو ليست تابعة أو معتمدة من قبل إنستغرام™ أو تيك توك™ أو يوتيوب™ أو فيسبوك™ أو أي منصة أخرى مذكورة. جميع العلامات التجارية ملك لأصحابها وتُستخدم هنا لأغراض وصفية فقط بموجب الاستخدام العادل الاسمي.
          </p>
        </div>
      </footer>
    </div>
  );
}
