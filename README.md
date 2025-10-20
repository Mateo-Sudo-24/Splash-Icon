# Guía Completa: Crear APK con Ionic + Angular

**Proyecto:** Splash-Icon

Esta guía detalla el proceso para crear una aplicación móvil utilizando Ionic con Angular, configurar íconos e imágenes de inicio personalizadas, editar el archivo AndroidManifest.xml, generar un APK funcional y subir todo a un repositorio en GitHub.

**Link de Descarga del APK:**  
https://epnecuador-my.sharepoint.com/:u:/g/personal/mateo_paredes_epn_edu_ec/EZ6lWLJvg7lKkrXvhTxtX70BvUAuiX1haSstxr23E0r39w?e=3D5dkm

---

## 1. Crear el proyecto Ionic

Crear un nuevo proyecto con la plantilla blank y soporte para Capacitor:
```bash
ionic start Splash-Icon blank --type=angular --capacitor
cd Splash-Icon
```

---

## 2. Configurar Capacitor

Instalar las dependencias necesarias e inicializar Capacitor:
```bash
npm install @capacitor/core @capacitor/cli --save
npx cap init "Splash-Icon" io.ionic.starter
```

Esto genera el archivo `capacitor.config.ts` con la configuración base del proyecto.

---

## 3. Construir la aplicación y añadir la plataforma Android

Compilar el proyecto y sincronizar con Android:
```bash
ionic build
npx cap add android
npx cap sync android
```

---

## 4. Configurar ícono y splash personalizados

### 4.1. Instalar generador de recursos
```bash
npm install --save-dev @capacitor/assets
```

### 4.2. Preparar imágenes base

Colocar las imágenes en la carpeta `resources/`:
```
resources/
├── icon.png      # 1024x1024 px
└── splash.png    # 2208x1242 px (recomendado)
```

### 4.3. Generar recursos
```bash
npx capacitor-assets generate
```

Esto crea los íconos y pantallas de inicio en `android/app/src/main/res/`.

---

## 5. Configuración de SplashScreen

Editar el archivo `capacitor.config.ts`:
```typescript
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
```

---

## 6. Editar AndroidManifest.xml

**Ruta del archivo:** `android/app/src/main/AndroidManifest.xml`

Agregar permisos necesarios:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.CAMERA" />
```

---

## 7. Probar en Android Studio

Abrir el proyecto nativo en Android Studio:
```bash
npx cap open android
```

### Pasos en Android Studio:

1. Seleccionar un emulador o dispositivo físico
2. Hacer clic en el botón de ejecución (▶) para instalar el APK de prueba
3. Verificar que el ícono y splash screen se muestren correctamente

---

## 8. Generar APK para distribución

### 8.1. En Android Studio:

1. Ir a **Build > Build Bundle(s) / APK(s) > Build APK(s)**
2. Esperar a que termine la compilación
3. Hacer clic en **locate** para encontrar el APK generado

### 8.2. Ubicación del APK:
```
android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 9. Subir el proyecto a GitHub

### 9.1. Inicializar repositorio Git
```bash
git init
git add .
git commit -m "Initial commit: Ionic + Angular project with custom splash and icon"
```

### 9.2. Conectar con repositorio remoto
```bash
git remote add origin https://github.com/tu-usuario/Splash-Icon.git
git branch -M main
git push -u origin main
```

---

## Notas adicionales

- Asegurarse de tener instalado Android Studio y las herramientas SDK necesarias
- Para generar un APK firmado para producción, seguir la documentación oficial de Android
- Verificar que Node.js, npm e Ionic CLI estén actualizados

---

## Recursos

- [Documentación oficial de Ionic](https://ionicframework.com/docs)
- [Documentación de Capacitor](https://capacitorjs.com/docs)
- [Guía de Android Studio](https://developer.android.com/studio)
