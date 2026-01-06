# From Zero To Hero

<div class="cover-hero">
  <h1>Red Hat OpenShift AI</h1>
  <h2>From Zero To Hero</h2>
  <p class="cover-description">A comprehensive journey from business use case to production-ready AI solution</p>
</div>

<div class="cover-team">
  <img src="images/portada-team.png" alt="Development Team" class="cover-team-image" />
  <img src="images/team-effort.png" alt="Team Effort" class="cover-team-image" />
</div>

<div class="cover-footer">
  <p class="cover-tagline">Building intelligent applications with MCP Agents, LlamaStack, and OpenShift AI</p>
</div>

<style>
.cover.show {
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 50%, #1a1a1a 100%) !important;
  position: relative;
  overflow: hidden;
}

.cover.show::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url('images/redhatone.svg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: 50%;
  opacity: 0.04;
  z-index: 0;
  filter: blur(3px);
  pointer-events: none;
}

.cover.show::after {
  content: '';
  position: absolute;
  top: -30%;
  right: -15%;
  width: 1000px;
  height: 1000px;
  background: radial-gradient(circle, rgba(204, 0, 0, 0.08) 0%, transparent 70%);
  border-radius: 50%;
  z-index: 0;
  pointer-events: none;
}

.cover.show .cover-main {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 2rem;
}

.cover-hero {
  text-align: center;
  z-index: 1;
  position: relative;
  margin-bottom: 3rem;
}

.cover.show h1 {
  font-family: 'RedHatDisplay', 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 4.5rem !important;
  font-weight: 700 !important;
  color: #FFFFFF !important;
  margin: 0 0 1rem 0 !important;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.5), 0 2px 8px rgba(204, 0, 0, 0.3) !important;
  letter-spacing: -0.02em !important;
  line-height: 1.1 !important;
}

.cover.show h2 {
  font-family: 'RedHatDisplay', 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 3rem !important;
  font-weight: 400 !important;
  color: #CC0000 !important;
  margin: 0 0 1.5rem 0 !important;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.4) !important;
  letter-spacing: 0.05em !important;
}

.cover-description {
  font-family: 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 1.5rem !important;
  color: #E8E8E8 !important;
  margin: 0 !important;
  font-weight: 300 !important;
  line-height: 1.6 !important;
  max-width: 800px !important;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.3) !important;
}

.cover-team {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  margin: 3rem 0;
  z-index: 1;
  position: relative;
  flex-wrap: wrap;
}

.cover-team-image {
  max-width: 400px;
  max-height: 300px;
  border-radius: 12px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4), 0 4px 16px rgba(204, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  object-fit: contain;
}

.cover-team-image:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.5), 0 6px 20px rgba(204, 0, 0, 0.3);
}

.cover-footer {
  text-align: center;
  z-index: 1;
  position: relative;
  margin-top: 2rem;
}

.cover-tagline {
  font-family: 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 1.2rem !important;
  color: #B8B8B8 !important;
  margin: 0 !important;
  font-weight: 300 !important;
  font-style: italic !important;
  text-shadow: 0 2px 6px rgba(0, 0, 0, 0.3) !important;
}

@keyframes subtleFade {
  0%, 100% {
    opacity: 0.04;
  }
  50% {
    opacity: 0.06;
  }
}

.cover.show::before {
  animation: subtleFade 8s ease-in-out infinite;
}

@media (max-width: 768px) {
  .cover.show h1 {
    font-size: 3rem !important;
  }
  
  .cover.show h2 {
    font-size: 2rem !important;
  }
  
  .cover-description {
    font-size: 1.2rem !important;
  }
  
  .cover-team {
    flex-direction: column;
    gap: 1.5rem;
  }
  
  .cover-team-image {
    max-width: 100%;
    max-height: 200px;
  }
}
</style>
