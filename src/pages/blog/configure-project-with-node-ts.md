---
layout: ../../layouts/Blog.astro
title: Guía Definitiva para Configurar un Proyecto Node.js con TypeScript
desc: Configura un proyecto Node.js con TypeScript fácilmente, optimizando tu desarrollo con tipado fuerte y autocompletado mejorado.
date: 22/10/24
image_path: /og/ts-node.webp
---

Configurar un proyecto Node.js con TypeScript permite aprovechar el tipado estático
para detectar errores antes de la ejecución, mejorar el autocompletado en editores,
facilitar la depuración y mantener una organización de código más clara y robusta,
lo que resulta en un desarrollo más eficiente y seguro.

## Primero crearemos una carpeta con el nombre del proyecto
```bash
mkdir name-proyect
cd name-proyect
```

## Dentro de nuestra carpeta inicializaremos un proyecto de node e instalamos las siguientes dependencias

```bash
npm init --yes
pnpm i
pnpm install -D typescript @types/node tsx
pnpm tsc --init
```
- *typescript*: El compilador de TypeScript, que convierte archivos .ts a JavaScript.
- *@types/node*: Proporciona definiciones de tipos para las APIs de Node.js, facilitando el autocompletado y el tipado en TypeScript.
- *tsx*: Una herramienta para ejecutar archivos TypeScript directamente sin necesidad de compilarlos previamente, ideal para el desarrollo.

## Ahora modificaremos el archivo de configuración de TypeScript
El archivo de configuración es este: `tsconfig.json`, borraremos todo lo que hay y pegaremos esto
```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "strict": true,
    "esModuleInterop": true,
    "allowImportingTsExtensions": false,
    "moduleResolution": "node"
  }
```
Esta configuración de TypeScript compila el código a JavaScript ES6, usa el sistema de módulos *commonjs* y
guarda los archivos compilados en la carpeta *dist*. Activa la verificación estricta de tipos con *strict*,
permite compatibilidad entre módulos CommonJS y ES (esModuleInterop), desactiva la importación de extensiones
*.ts* (*allowImportingTsExtensions*), y utiliza la resolución de módulos de estilo Node.js
(*moduleResolution: "node"*).

## Y por último en el archivo `package.json` añadiremos lo siguiente en el apartado de *scripts*
```json
"scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "tsx watch index.ts", // Cambia el nombre del archivo por el tuyo
  },
```

- *build*: Ejecuta tsc (TypeScript Compiler) para compilar todos los archivos .ts a JavaScript, generando los archivos en la carpeta dist.
- *start*: Inicia la aplicación usando Node.js y ejecuta el archivo index.js desde la carpeta dist, ideal para entornos de producción.
- *dev*: Utiliza tsx para ejecutar el archivo index.ts en modo de desarrollo, vigilando los cambios en tiempo real y recargando automáticamente cuando se modifica el código.
