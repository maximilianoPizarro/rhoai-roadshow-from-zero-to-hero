# From Zero To Hero

Welcome to **Red Hat OpenShift AI From Zero To Hero** - a comprehensive journey from business use case to production-ready AI solution.

<img src="images/portada-team.png" alt="Red Hat OpenShift AI From Zero To Hero" class="cover-portada-image" />

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

.cover.show h1 {
  font-family: 'RedHatDisplay', 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 5rem !important;
  font-weight: 700 !important;
  color: #CC0000 !important;
  margin: 0 0 1.5rem 0 !important;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.8), 0 2px 10px rgba(204, 0, 0, 0.5) !important;
  letter-spacing: -0.02em !important;
  line-height: 1.1 !important;
  text-align: center !important;
}

.cover.show p {
  font-family: 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 1.8rem !important;
  color: #FFFFFF !important;
  margin: 2rem 0 3rem 0 !important;
  font-weight: 400 !important;
  line-height: 1.7 !important;
  max-width: 900px !important;
  text-shadow: 0 3px 12px rgba(0, 0, 0, 0.6), 0 1px 4px rgba(0, 0, 0, 0.4) !important;
  text-align: center !important;
  background: rgba(0, 0, 0, 0.3);
  padding: 1.5rem 2rem;
  border-radius: 8px;
  border-left: 4px solid #CC0000;
}

.cover-portada-image {
  max-width: 800px;
  width: 100%;
  height: auto;
  border-radius: 16px;
  box-shadow: 0 12px 48px rgba(0, 0, 0, 0.5), 0 6px 24px rgba(204, 0, 0, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  object-fit: contain;
  margin-top: 2rem;
  z-index: 1;
  position: relative;
}

.cover-portada-image:hover {
  transform: translateY(-8px);
  box-shadow: 0 16px 56px rgba(0, 0, 0, 0.6), 0 8px 28px rgba(204, 0, 0, 0.4);
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
    font-size: 3.5rem !important;
  }
  
  .cover.show p {
    font-size: 1.3rem !important;
    padding: 1rem 1.5rem !important;
  }
  
  .cover-portada-image {
    max-width: 100%;
    margin-top: 1.5rem;
  }
}
</style>
