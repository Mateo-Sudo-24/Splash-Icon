#Guía completa: Crear APK con Ionic + Angular

#Proyecto: Splash-Icon
Esta guía explica cómo crear una app móvil con Ionic Angular, configurar ícono y splash personalizados, editar el AndroidManifest.xml, generar un APK funcional y subirlo a GitHub.

1. Crear el proyecto Ionic
Shellionic start Splash-Icon blank --type=angular --capacitorcd Splash-IconMostrar más líneas

2. Configurar Capacitor
Si no lo hiciste con --capacitor, puedes hacerlo manualmente:
Shellnpm install @capacitor/core @capacitor/cli --savenpx cap init "Splash-Icon" io.ionic.starterMostrar más líneas

3. Construir la app y añadir Android
Shellionic buildnpx cap add androidnpx cap sync android``Mostrar más líneas

4. Ícono y Splash personalizados
Instalación del generador de recursos:
Shellnpm install --save-dev @capacitor/assetsMostrar más líneas
Estructura de imágenes:
resources/
├── icon.png      # 1024x1024
└── splash.png    # 2208x1242 (recomendado)

Generar recursos:

npx capacitor-assets generateMostrar más líneas

Esto crea los íconos y splash en android/app/src/main/res/.

5. Configuración en capacitor.config.ts

import type { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'io.ionic.starter',
  appName: 'Splash-Icon',
  webDir: 'www',
  bundledWebRuntime: false,
  plugins: {
     SplashScreen: {
      launchShowDuration: 5000,
      launchAutoHide: true,
      backgroundColor: "#ffffffff",
      androidSplashResourceName: "splash",
      androidScaleType: "FIT_CENTER",
      showSpinner: false,
      splashFullScreen: true,
      splashImmersive: true,
    }
  }
};

export default config;

6. Editar AndroidManifest.xml
Ruta: android/app/src/main/AndroidManifest.xml
Ejemplo de permisos:
XML<uses-permission android:name="android.permission.INTERNET" /><uses-permission android:name="android.permission.CAMERA" />Mostrar más líneas

7. Probar en Android Studio
   
npx cap open androidMostrar más líneas

En Android Studio:

Selecciona un emulador o dispositivo físico

Haz clic en ▶ para instalar el APK de prueba

8. Generar APK para entrega
En Android Studio:

<img width="411" height="787" alt="image" src="https://github.com/user-attachments/assets/ebf9ce49-ed49-4e25-a113-35e05f9b95c1" />
