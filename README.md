"use client";

import { useEffect, useRef } from "react";
import Link from "next/link";

// ------------------------------------------------------
// Drop this file into: app/page.tsx (Next.js App Router)
// Tailwind required. Optional: shadcn/ui not required.
// ------------------------------------------------------

export default function PortfolioPage() {
  return (
    <main className="min-h-screen bg-[#0B0F14] text-slate-200 antialiased">
      <Hero />
      <Tech />
      <Projects />
      <Strengths />
      <Stats />
      <Contact />
      <Footer />
    </main>
  );
}

// -------------------- Hero ----------------------------
function Hero() {
  return (
    <section className="relative overflow-hidden">
      {/* gradient backdrop */}
      <div className="pointer-events-none absolute inset-0 -z-10">
        <div className="absolute -top-40 left-1/2 h-[44rem] w-[44rem] -translate-x-1/2 rounded-full bg-[radial-gradient(circle_at_center,rgba(0,255,255,0.15),transparent_60%)] blur-3xl" />
        <div className="absolute bottom-0 left-0 right-0 mx-auto h-[20rem] w-full bg-[linear-gradient(to_top,rgba(11,15,20,1),rgba(11,15,20,0))]" />
      </div>

      <div className="mx-auto max-w-6xl px-5 pb-16 pt-28 md:pt-32">
        <div className="flex flex-col items-center text-center">
          <h1 className="text-3xl font-semibold tracking-tight text-cyan-300 md:text-5xl">
            Narasimha Reddy Putta
          </h1>
          <p className="mt-3 text-lg text-slate-300 md:text-xl">
            Software Development Engineer — Java, Cloud & Distributed Systems
          </p>
          <Typer
            lines={[
              "Building scalable backend systems and cloud‑native apps",
              "Turning complexity into elegant, production‑ready solutions",
              "MSc Computer Science @ DePaul University, Chicago",
            ]}
          />

        <div className="mt-8 flex flex-wrap items-center justify-center gap-3">
            <CTA href="https://www.linkedin.com/in/narasimhareddy94/" label="LinkedIn" />
            <CTA href="https://github.com/narasimhareddyputta94" label="GitHub" variant="ghost" />
            <CTA href="mailto:narasimhareddyputta94@gmail.com" label="Email" variant="ghost" />
          </div>
        </div>
      </div>
    </section>
  );
}

// Simple typewriter without external deps
function Typer({ lines }: { lines: string[] }) {
  const spanRef = useRef<HTMLSpanElement>(null);
  useEffect(() => {
    const el = spanRef.current;
    if (!el) return;

    let i = 0; // which line
    let j = 0; // char index
    let deleting = false;

    const tick = () => {
      const current = lines[i] ?? "";
      const visible = deleting ? current.slice(0, j--) : current.slice(0, j++);
      el.textContent = visible;

      const atEnd = j >= current.length;
      const atStart = j <= 0;

      let delay = deleting ? 18 : 32; // typing speed
      if (atEnd) {
        delay = 1400; // pause on full line
        deleting = true;
      } else if (atStart && deleting) {
        deleting = false;
        i = (i + 1) % lines.length;
        delay = 300;
      }
      timer = window.setTimeout(tick, delay);
    };

    let timer = window.setTimeout(tick, 300);
    return () => window.clearTimeout(timer);
  }, [lines]);

  return (
    <p className="mt-6 max-w-3xl text-balance text-center text-slate-400">
      <span ref={spanRef} className="border-r border-cyan-400 pr-1" />
    </p>
  );
}

function CTA({
  href,
  label,
  variant = "solid",
}: {
  href: string;
  label: string;
  variant?: "solid" | "ghost";
}) {
  return (
    <Link
      href={href}
      className={
        variant === "solid"
          ? "rounded-2xl bg-cyan-400/10 px-4 py-2 text-cyan-300 ring-1 ring-cyan-400/40 transition hover:bg-cyan-400/20"
          : "rounded-2xl px-4 py-2 text-slate-300 ring-1 ring-slate-600/60 transition hover:bg-white/5"
      }
    >
      {label}
    </Link>
  );
}

// -------------------- Tech ----------------------------
function Tech() {
  return (
    <section className="mx-auto max-w-6xl px-5 py-12">
      <h2 className="text-xl font-semibold text-slate-100 md:text-2xl">Technical Expertise</h2>

      <div className="mt-6 grid gap-6 md:grid-cols-3">
        <Card title="Core Stack" subtitle="Languages & Frameworks">
          <Badge src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java" />
          <Badge src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" alt="Spring Boot" />
          <Badge src="https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54" alt="Python" />
          <Badge src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
          <Badge src="https://img.shields.io/badge/React-20232a?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
          <Badge src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js" />
        </Card>

        <Card title="Data & Middleware" subtitle="Storage, Search & Streams">
          <Badge src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />
          <Badge src="https://img.shields.io/badge/MySQL-00758F?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
          <Badge src="https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
          <Badge src="https://img.shields.io/badge/Kafka-231F20?style=for-the-badge&logo=apachekafka&logoColor=white" alt="Kafka" />
          <Badge src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white" alt="Elasticsearch" />
          <Badge src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="Redis" />
        </Card>

        <Card title="Cloud & DevOps" subtitle="Infra, Containers & CI/CD">
          <Badge src="https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="AWS" />
          <Badge src="https://img.shields.io/badge/Docker-0db7ed?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
          <Badge src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" alt="Kubernetes" />
          <Badge src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="GitHub Actions" />
          <Badge src="https://img.shields.io/badge/CI%2FCD-Pipelines-111827?style=for-the-badge&logo=gitlab&logoColor=white" alt="CI/CD" />
          <Badge src="https://img.shields.io/badge/OAuth2-3B3B3B?style=for-the-badge&logo=auth0&logoColor=white" alt="OAuth2" />
        </Card>
      </div>
    </section>
  );
}

function Card({
  title,
  subtitle,
  children,
}: {
  title: string;
  subtitle?: string;
  children: React.ReactNode;
}) {
  return (
    <div className="rounded-2xl border border-white/10 bg-white/5 p-5 shadow-[0_0_1px_0_rgba(255,255,255,0.15)]">
      <div className="mb-4">
        <h3 className="text-lg font-medium text-slate-100">{title}</h3>
        {subtitle ? (
          <p className="text-sm text-slate-400">{subtitle}</p>
        ) : null}
      </div>
      <div className="flex flex-wrap gap-2">{children}</div>
    </div>
  );
}

function Badge({ src, alt }: { src: string; alt: string }) {
  return (
    // eslint-disable-next-line @next/next/no-img-element
    <img src={src} alt={alt} className="h-8 select-none rounded-md" />
  );
}

// -------------------- Projects ------------------------
function Projects() {
  const data: Project[] = [
    {
      title: "E‑Commerce Cloud Suite",
      impact:
        "40% faster checkout and zero‑downtime releases with event‑driven microservices and Elasticsearch search.",
      bullets: [
        "Spring Boot services on AWS ECS/EKS; Kafka for order/event streams",
        "Elasticsearch for full‑text search & analytics",
        "Kubernetes for autoscaling and resilience",
      ],
      stack: "Java · Spring Boot · Angular · Kafka · AWS · Kubernetes · OAuth2",
    },
    {
      title: "Enterprise Resource Planning (ERP)",
      impact:
        "Reduced manual ops by 30% through modular microservices and automation across HR, inventory, and finance.",
      bullets: [
        "Deployed on AWS EKS with Docker; HPA for horizontal scaling",
        "Optimized SQL and caching for faster workflows",
        "Role‑based access control with OAuth2",
      ],
      stack: "Java · React · PostgreSQL · Docker · AWS",
    },
    {
      title: "Inventory & Order Management System",
      impact:
        "Sub‑second query performance and real‑time stock accuracy across branches.",
      bullets: [
        "Kafka streams for live synchronization",
        "Elasticsearch indices for instant lookups",
        "Angular dashboards for trends and SLAs",
      ],
      stack: "Java · Angular · Kafka · MySQL · Elasticsearch",
    },
    {
      title: "Online Banking System",
      impact:
        "Lowered transaction latency by 25% with optimized indexing and async pipelines.",
      bullets: [
        "Spring Security + OAuth2 with MFA",
        "Kafka for immutable audit logs",
        "PostgreSQL for ACID transactions",
      ],
      stack: "Java · Spring Boot · PostgreSQL · Kafka · Spring Security",
    },
  ];

  return (
    <section className="mx-auto max-w-6xl px-5 py-12">
      <div className="mb-6 flex items-end justify-between">
        <h2 className="text-xl font-semibold text-slate-100 md:text-2xl">Featured Projects</h2>
        <Link
          href="https://github.com/narasimhareddyputta94"
          className="text-sm text-cyan-300 underline underline-offset-4 hover:text-cyan-200"
        >
          View GitHub
        </Link>
      </div>

      <div className="grid gap-6 md:grid-cols-2">
        {data.map((p) => (
          <ProjectCard key={p.title} {...p} />
        ))}
      </div>
    </section>
  );
}

type Project = {
  title: string;
  impact: string;
  bullets: string[];
  stack: string;
};

function ProjectCard({ title, impact, bullets, stack }: Project) {
  return (
    <article className="group rounded-2xl border border-white/10 bg-gradient-to-b from-white/5 to-white/0 p-6 transition hover:border-cyan-400/40">
      <h3 className="text-lg font-medium text-slate-100">{title}</h3>
      <p className="mt-2 text-sm text-slate-400">{impact}</p>
      <ul className="mt-4 list-disc space-y-1 pl-5 text-sm text-slate-300">
        {bullets.map((b) => (
          <li key={b}>{b}</li>
        ))}
      </ul>
      <p className="mt-4 text-xs tracking-wide text-slate-400">{stack}</p>
    </article>
  );
}

// -------------------- Strengths -----------------------
function Strengths() {
  const items = [
    {
      title: "Backend Engineering",
      desc: "RESTful APIs, Spring Boot microservices, async processing with Kafka",
    },
    {
      title: "System Design",
      desc: "Event‑driven architectures, fault tolerance, observability, scalability",
    },
    {
      title: "Cloud Infrastructure",
      desc: "AWS EC2/EKS/S3, containerization, GitHub Actions CI/CD",
    },
    {
      title: "Data Management",
      desc: "Relational & NoSQL modeling, indexing, caching, Elasticsearch",
    },
    { title: "Security", desc: "OAuth2, JWT, RBAC, secure API design" },
    { title: "Collaboration", desc: "Agile, documentation, mentorship" },
  ];

  return (
    <section className="mx-auto max-w-6xl px-5 py-12">
      <h2 className="text-xl font-semibold text-slate-100 md:text-2xl">Core Strengths</h2>
      <div className="mt-6 grid gap-4 md:grid-cols-2 lg:grid-cols-3">
        {items.map((s) => (
          <div
            key={s.title}
            className="rounded-2xl border border-white/10 bg-white/5 p-5"
          >
            <h3 className="text-base font-medium text-slate-100">{s.title}</h3>
            <p className="mt-1 text-sm text-slate-400">{s.desc}</p>
          </div>
        ))}
      </div>
    </section>
  );
}

// -------------------- Stats ---------------------------
function Stats() {
  return (
    <section className="mx-auto max-w-6xl px-5 py-12">
      <h2 className="text-xl font-semibold text-slate-100 md:text-2xl">GitHub Analytics</h2>
      <div className="mt-6 grid gap-6 md:grid-cols-2">
        {/* eslint-disable-next-line @next/next/no-img-element */}
        <img
          src="https://github-readme-streak-stats.herokuapp.com?user=narasimhareddyputta94&theme=tokyonight&hide_border=true"
          alt="GitHub Streak"
          className="w-full rounded-2xl border border-white/10 bg-white/5 p-3"
        />
        {/* eslint-disable-next-line @next/next/no-img-element */}
        <img
          src="https://github-readme-stats.vercel.app/api/top-langs/?username=narasimhareddyputta94&layout=compact&theme=tokyonight&hide_border=true"
          alt="Top Languages"
          className="w-full rounded-2xl border border-white/10 bg-white/5 p-3"
        />
      </div>
    </section>
  );
}

// -------------------- Contact ------------------------
function Contact() {
  return (
    <section className="mx-auto max-w-6xl px-5 py-14">
      <div className="rounded-3xl border border-cyan-400/30 bg-gradient-to-b from-cyan-400/10 to-transparent p-8 text-center">
        <h2 className="text-2xl font-semibold text-cyan-300 md:text-3xl">
          Let’s connect
        </h2>
        <p className="mx-auto mt-2 max-w-2xl text-slate-300">
          I’m actively seeking opportunities in Software Engineering and Cloud Solutions. If my work resonates, reach out — I’d love to collaborate.
        </p>
        <div className="mt-6 flex flex-wrap items-center justify-center gap-3">
          <CTA href="mailto:narasimhareddyputta94@gmail.com" label="Email" />
          <CTA href="https://www.linkedin.com/in/narasimhareddy94/" label="LinkedIn" variant="ghost" />
          <CTA href="https://github.com/narasimhareddyputta94" label="GitHub" variant="ghost" />
        </div>
      </div>
    </section>
  );
}

// -------------------- Footer -------------------------
function Footer() {
  return (
    <footer className="border-t border-white/10 py-8">
      <div className="mx-auto flex max-w-6xl flex-col items-center justify-between gap-2 px-5 text-sm text-slate-400 md:flex-row">
        <p>
          © {new Date().getFullYear()} Narasimha Reddy Putta • Built with Next.js & Tailwind
        </p>
        <nav className="flex items-center gap-5">
          <Link href="#" className="hover:text-slate-200">
            Resume (add link)
          </Link>
          <Link href="https://www.linkedin.com/in/narasimhareddy94/" className="hover:text-slate-200">
            LinkedIn
          </Link>
          <Link href="mailto:narasimhareddyputta94@gmail.com" className="hover:text-slate-200">
            Email
          </Link>
        </nav>
      </div>
    </footer>
  );
}
