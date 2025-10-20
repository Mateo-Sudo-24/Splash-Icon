Guía completa: Crear APK con Ionic + Angular

Proyecto: Splash-Icon

Esta guía detalla el proceso para crear una aplicación móvil utilizando Ionic con Angular, configurar íconos e imágenes de inicio personalizadas, editar el archivo AndroidManifest.xml, generar un APK funcional y subir todo a un repositorio en GitHub.

Link De Descarga del APK: https://epnecuador-my.sharepoint.com/:u:/g/personal/mateo_paredes_epn_edu_ec/EZ6lWLJvg7lKkrXvhTxtX70BvUAuiX1haSstxr23E0r39w?e=3D5dkm

1. Crear el proyecto Ionic
Usamos la plantilla blank con soporte para Capacitor:
Shellionic start Splash-Icon blank --type=angular --capacitorcd Splash-IconMostrar más líneas

2. Configurar Capacitor (si no se hizo en el paso anterior)
Shellnpm install @capacitor/core @capacitor/cli --savenpx cap init "Splash-Icon" io.ionic.starterMostrar más líneas
Esto genera el archivo capacitor.config.ts con la configuración base del proyecto.

3. Construir la aplicación y añadir la plataforma Android
Shellionic buildnpx cap add androidnpx cap sync androidMostrar más líneas

4. Ícono y Splash personalizados
Instalamos el generador oficial de recursos:
Shellnpm install --save-dev @capacitor/assetsMostrar más líneas
Colocamos las imágenes base en la carpeta resources/:
resources/
├── icon.png      # 1024x1024
└── splash.png    # 2208x1242 (recomendado)

Generamos los recursos:
Shellnpx capacitor-assets generateMostrar más líneas
Esto crea los íconos y pantallas de inicio en android/app/src/main/res/.

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
Ruta del archivo: android/app/src/main/AndroidManifest.xml
Ejemplo de permisos:
XML<uses-permission android:name="android.permission.INTERNET" /><uses-permission android:name="android.permission.CAMERA" />Mostrar más líneas

7. Probar en Android Studio
Abrimos el proyecto nativo:
Shellnpx cap open androidMostrar más líneas
En Android Studio:

Selecciona un emulador o dispositivo físico
Haz clic en el botón de ejecución (▶) para instalar el APK de prueba


8. Generar APK para entrega
En Android Studio:
<img width="411" height="787" alt="image" src="https://github.com/user-attachments/assets/b198675e-4eaf-4b6a-8abb-a566a14e3c0a" />

