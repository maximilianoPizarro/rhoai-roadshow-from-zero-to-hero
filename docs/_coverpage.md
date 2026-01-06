# From Zero To Hero

Welcome to **Red Hat OpenShift AI From Zero To Hero** - a comprehensive journey from business use case to production-ready AI solution.

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
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.cover.show h1 {
  font-family: 'RedHatDisplay', 'RedHatText', Overpass, 'Open Sans', Helvetica, Arial, sans-serif !important;
  font-size: 4rem !important;
  font-weight: 700 !important;
  color: #FFFFFF !important;
  margin: 0 0 1rem 0 !important;
  text-shadow: 0 6px 24px rgba(0, 0, 0, 0.9), 0 3px 12px rgba(204, 0, 0, 0.7), 0 0 50px rgba(204, 0, 0, 0.4), 2px 2px 4px rgba(0, 0, 0, 0.8) !important;
  letter-spacing: -0.01em !important;
  line-height: 1.2 !important;
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
  .cover.show .cover-main {
    max-width: 100%;
    padding: 1.5rem;
  }
  
  .cover.show h1 {
    font-size: 2.5rem !important;
  }
  
  .cover.show p {
    font-size: 1.2rem !important;
    padding: 1rem 1.5rem !important;
    max-width: 100% !important;
  }
}
</style>
