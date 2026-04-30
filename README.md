[script.js](https://github.com/user-attachments/files/27235650/script.js)
// ===== MOBILE MENU TOGGLE =====
function toggleMenu() {
  const navLinks = document.querySelector('.nav-links');
  navLinks.classList.toggle('open');
}

// Close menu when a link is clicked
document.querySelectorAll('.nav-links a').forEach(link => {
  link.addEventListener('click', () => {
    document.querySelector('.nav-links').classList.remove('open');
  });
});

// ===== CONTACT FORM =====
function sendMessage() {
  const name = document.getElementById('nameInput').value.trim();
  const email = document.getElementById('emailInput').value.trim();
  const msg = document.getElementById('msgInput').value.trim();
  const formMsg = document.getElementById('formMsg');

  if (!name || !email || !msg) {
    formMsg.style.color = '#ff6584';
    formMsg.textContent = '⚠️ Please fill in all fields!';
    return;
  }

  if (!email.includes('@')) {
    formMsg.style.color = '#ff6584';
    formMsg.textContent = '⚠️ Please enter a valid email!';
    return;
  }

  formMsg.style.color = '#6c63ff';
  formMsg.textContent = `✅ Thanks ${name}! Your message has been sent.`;

  // Clear fields
  document.getElementById('nameInput').value = '';
  document.getElementById('emailInput').value = '';
  document.getElementById('msgInput').value = '';

  setTimeout(() => { formMsg.textContent = ''; }, 4000);
}

// ===== SCROLL ANIMATION =====
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.style.opacity = '1';
      entry.target.style.transform = 'translateY(0)';
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.about-card, .skill-item').forEach(el => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(30px)';
  el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
  observer.observe(el);
});

// ===== ACTIVE NAV HIGHLIGHT =====
window.addEventListener('scroll', () => {
  const sections = document.querySelectorAll('section');
  const navLinks = document.querySelectorAll('.nav-links a');

  sections.forEach((section, i) => {
    const rect = section.getBoundingClientRect();
    if (rect.top <= 80 && rect.bottom >= 80) {
      navLinks.forEach(l => l.style.color = '#ccc');
      if (navLinks[i]) navLinks[i].style.color = '#6c63ff';
    }
  });
});
