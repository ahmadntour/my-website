/* ============================================
   AHMAD NATOUR — script.js
   Scroll Animations, Navbar, Mobile Menu
   ============================================ */

(function () {
  'use strict';

  // ── Navbar scroll behavior ──────────────────
  const navbar = document.getElementById('navbar');
  let lastScroll = 0;

  function handleNavbar() {
    const scrollY = window.scrollY;
    if (scrollY > 40) {
      navbar.classList.add('scrolled');
    } else {
      navbar.classList.remove('scrolled');
    }
    lastScroll = scrollY;
  }

  window.addEventListener('scroll', handleNavbar, { passive: true });
  handleNavbar();

  // ── Mobile menu ─────────────────────────────
  const hamburger = document.getElementById('hamburger');
  const mobileMenu = document.getElementById('mobileMenu');
  let menuOpen = false;

  hamburger.addEventListener('click', () => {
    menuOpen = !menuOpen;
    mobileMenu.classList.toggle('open', menuOpen);
    hamburger.setAttribute('aria-expanded', menuOpen);
  });

  // Close mobile menu on link click
  mobileMenu.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      menuOpen = false;
      mobileMenu.classList.remove('open');
    });
  });

  // ── Reveal on scroll ────────────────────────
  const reveals = document.querySelectorAll('.reveal');

  const revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    },
    {
      threshold: 0.12,
      rootMargin: '0px 0px -40px 0px'
    }
  );

  reveals.forEach(el => revealObserver.observe(el));

  // ── Smooth scroll for anchor links ──────────
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
      const href = this.getAttribute('href');
      if (href === '#') return;
      const target = document.querySelector(href);
      if (!target) return;
      e.preventDefault();
      const navH = parseInt(getComputedStyle(document.documentElement).getPropertyValue('--nav-h') || '76');
      const top = target.getBoundingClientRect().top + window.scrollY - navH - 16;
      window.scrollTo({ top, behavior: 'smooth' });
    });
  });

  // ── Active nav link highlight ───────────────
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-links a');

  function activateNavLink() {
    const scrollY = window.scrollY;
    sections.forEach(section => {
      const sTop = section.offsetTop - 120;
      const sBot = sTop + section.offsetHeight;
      if (scrollY >= sTop && scrollY < sBot) {
        const id = section.getAttribute('id');
        navLinks.forEach(link => {
          link.classList.remove('active');
          if (link.getAttribute('href') === `#${id}`) {
            link.classList.add('active');
          }
        });
      }
    });
  }

  window.addEventListener('scroll', activateNavLink, { passive: true });

  // ── WhatsApp float tooltip direction fix ────
  // Ensure tooltip doesn't overflow on small screens
  const waFloat = document.querySelector('.whatsapp-float');
  if (waFloat) {
    function adjustTooltip() {
      const tooltip = waFloat.querySelector('.wa-tooltip');
      if (!tooltip) return;
      const rect = waFloat.getBoundingClientRect();
      if (rect.left < 120) {
        tooltip.style.right = 'auto';
        tooltip.style.left = 'calc(100% + 12px)';
      }
    }
    adjustTooltip();
    window.addEventListener('resize', adjustTooltip, { passive: true });
  }

  // ── Staggered counter animation for stats ───
  function animateValue(el, start, end, duration, suffix) {
    let startTime = null;
    function step(timestamp) {
      if (!startTime) startTime = timestamp;
      const progress = Math.min((timestamp - startTime) / duration, 1);
      const eased = 1 - Math.pow(1 - progress, 3);
      el.textContent = Math.floor(eased * (end - start) + start) + suffix;
      if (progress < 1) requestAnimationFrame(step);
    }
    requestAnimationFrame(step);
  }

  // ── Lazy load images ─────────────────────────
  const lazyImages = document.querySelectorAll('img[loading="lazy"]');
  if ('IntersectionObserver' in window) {
    const imgObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const img = entry.target;
          img.src = img.dataset.src || img.src;
          imgObserver.unobserve(img);
        }
      });
    });
    lazyImages.forEach(img => imgObserver.observe(img));
  }

  // ── Page load polish ─────────────────────────
  window.addEventListener('load', () => {
    document.body.style.opacity = '0';
    document.body.style.transition = 'opacity 0.4s ease';
    requestAnimationFrame(() => {
      document.body.style.opacity = '1';
    });
  });

})();
