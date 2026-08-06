<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>wizwazwuz</title>
  <style>
    /* Global Styles */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      background-color: #0d1b2a; /* Dark Blue */
      color: #4ecdc4; /* Teal */
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      overflow-x: hidden;
    }

    /* Main Container & 3D Setup */
    .hero-container {
      position: relative;
      perspective: 1000px;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
    }

    .float-wrapper {
      animation: gentleFloat 4s ease-in-out infinite alternate;
      transform-style: preserve-3d;
    }

    .tilt-card {
      transition: transform 0.1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
      transform-style: preserve-3d;
      cursor: pointer;
      user-select: none;
    }

    /* 3D Title Styling */
    .title-logo {
      font-size: clamp(3rem, 10vw, 7rem);
      font-weight: 900;
      letter-spacing: 2px;
      color: #4ecdc4;
      text-shadow: 
        0px 10px 20px rgba(0, 0, 0, 0.5),
        0px 0px 30px rgba(78, 205, 196, 0.3);
      padding: 10px 20px;
    }

    /* Navigation Buttons */
    .nav-buttons {
      margin-top: 25px;
      display: flex;
      gap: 15px;
      align-items: center;
      z-index: 10;
    }

    .nav-btn {
      background: transparent;
      border: 2px solid #4ecdc4;
      color: #4ecdc4;
      font-size: 0.9rem;
      font-weight: 700;
      letter-spacing: 2px;
      padding: 10px 20px;
      border-radius: 25px;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .nav-btn:hover {
      background-color: #4ecdc4;
      color: #0d1b2a;
      box-shadow: 0 0 15px rgba(78, 205, 196, 0.4);
      transform: translateY(-2px);
    }

    .divider {
      color: #1b263b;
      font-size: 1.2rem;
    }

    /* Modal Backdrop Dark Effect */
    .modal-backdrop {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(5, 10, 18, 0.75);
      backdrop-filter: blur(8px);
      display: flex;
      justify-content: center;
      align-items: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
      z-index: 100;
    }

    .modal-backdrop.active {
      opacity: 1;
      pointer-events: auto;
    }

    /* Popup Frame */
    .modal-frame {
      background: #1b263b;
      border: 1px solid rgba(78, 205, 196, 0.3);
      width: 90%;
      max-width: 700px;
      max-height: 80vh;
      border-radius: 16px;
      padding: 30px;
      overflow-y: auto;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6);
      transform: scale(0.8) translateY(20px);
      transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      position: relative;
    }

    .modal-backdrop.active .modal-frame {
      transform: scale(1) translateY(0);
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      border-bottom: 1px solid rgba(78, 205, 196, 0.2);
      padding-bottom: 10px;
    }

    .modal-title {
      font-size: 1.5rem;
      text-transform: uppercase;
      letter-spacing: 1.5px;
    }

    .close-btn {
      background: none;
      border: none;
      color: #4ecdc4;
      font-size: 1.8rem;
      cursor: pointer;
      line-height: 1;
    }

    /* Content Layouts Inside Modals */
    .about-text {
      line-height: 1.8;
      color: #e0e1dd;
      font-size: 1rem;
    }

    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 20px;
    }

    .project-card {
      background: #0d1b2a;
      border: 1px solid rgba(78, 205, 196, 0.2);
      border-radius: 10px;
      padding: 20px;
      transition: transform 0.2s ease, border-color 0.2s ease;
    }

    .project-card:hover {
      transform: translateY(-5px);
      border-color: #4ecdc4;
    }

    .project-card h3 {
      font-size: 1.1rem;
      margin-bottom: 8px;
    }

    .project-card p {
      font-size: 0.85rem;
      color: #e0e1dd;
      line-height: 1.4;
    }

    /* Idle Float Keyframes */
    @keyframes gentleFloat {
      0% { transform: translateY(0px) rotate(0deg); }
      100% { transform: translateY(-10px) rotate(0.5deg); }
    }
  </style>
</head>
<body>

  <!-- Main Display -->
  <div class="hero-container" id="heroContainer">
    <div class="float-wrapper">
      <div class="tilt-card" id="tiltCard">
        <h1 class="title-logo">wizwazwuz</h1>
      </div>
    </div>

    <!-- Navigation -->
    <div class="nav-buttons">
      <button class="nav-btn" onclick="openModal('projectsModal')">PROJECTS</button>
      <span class="divider">•</span>
      <button class="nav-btn" onclick="openModal('aboutModal')">ABOUT</button>
    </div>
  </div>

  <!-- Projects Modal -->
  <div class="modal-backdrop" id="projectsModal" onclick="closeModalOnOutsideClick(event, 'projectsModal')">
    <div class="modal-frame">
      <div class="modal-header">
        <h2 class="modal-title">Projects</h2>
        <button class="close-btn" onclick="closeModal('projectsModal')">&times;</button>
      </div>
      <div class="projects-grid">
        <!-- Duplicate this block to add more projects -->
        <div class="project-card">
          <h3>Project One</h3>
          <p>Description of your first awesome project goes here.</p>
        </div>
        <div class="project-card">
          <h3>Project Two</h3>
          <p>Description of your second project goes here.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- About Modal -->
  <div class="modal-backdrop" id="aboutModal" onclick="closeModalOnOutsideClick(event, 'aboutModal')">
    <div class="modal-frame">
      <div class="modal-header">
        <h2 class="modal-title">About</h2>
        <button class="close-btn" onclick="closeModal('aboutModal')">&times;</button>
      </div>
      <p class="about-text">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </p>
    </div>
  </div>

  <script>
    // 3D Tilt Effect
    const card = document.getElementById('tiltCard');
    const container = document.getElementById('heroContainer');
    const MAX_TILT = 20;

    container.addEventListener('mousemove', (e) => {
      const rect = container.getBoundingClientRect();
      const x = (e.clientX - rect.left) / rect.width - 0.5;
      const y = (e.clientY - rect.top) / rect.height - 0.5;

      const rotateX = -y * MAX_TILT;
      const rotateY = x * MAX_TILT;

      card.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.05)`;
    });

    container.addEventListener('mouseleave', () => {
      card.style.transform = 'rotateX(0deg) rotateY(0deg) scale(1)';
    });

    // Modal Control Functions
    function openModal(id) {
      document.getElementById(id).classList.add('active');
    }

    function closeModal(id) {
      document.getElementById(id).classList.remove('active');
    }

    // Close Modal When Clicking Outside Frame
    function closeModalOnOutsideClick(event, id) {
      if (event.target.classList.contains('modal-backdrop')) {
        closeModal(id);
      }
    }
  </script>

</body>
</html>
