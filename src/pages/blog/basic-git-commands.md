---
layout: ../../layouts/Blog.astro
title: Comandos básicos de git 
desc: Guía rápida de los comandos esenciales de Git para gestionar tus proyectos con control de versiones.
date: 17/09/2024
image_path: /og/git.webp
---

Aprende los comandos básicos de Git que todo desarrollador debe conocer para gestionar el control de versiones de sus proyectos.
Desde la inicialización de un repositorio hasta la sincronización con un servidor remoto, este artículo
te guiará paso a paso para que puedas comenzar a usar Git con confianza.

## ¿Qué es git?
> Es un  sistema de control de versiones distribuido que te permite registrar los cambios que haces en tus archivos y
volver a versiones anteriores si algo sale mal. - Freddy Vega

## Instalación
```bash
brew install git
```

## Crear repositorio
```bash
git init
```
Inicializa un nuevo repositorio Git en el directorio actual. Crea un nuevo subdirectorio .git que contiene todos los archivos necesarios para el repositorio.

## Clonar un Repositorio
```bash
git clone <url-del-repositorio>
```
Clona un repositorio remoto en tu máquina local. Sustituye <url-del-repositorio> por la URL del repositorio que deseas clonar.

## Verificar el Estado de los Archivos
```bash
git status
```
Este comando muestra el estado actual de los archivos en el repositorio, indicando qué archivos han sido modificados o no están siendo seguidos.

## Agregar Archivos al Área de Preparación
```bash
git add <archivo>
```
Este comando añade un archivo específico al área de preparación, preparándolo para el siguiente commit. Puedes usar `.` para agregar todos los archivos modificados.

## Confirmar Cambios
```bash
git commit -m "Mensaje del commit"
```
Este comando guarda los cambios agregados al área de preparación. Debes proporcionar un mensaje descriptivo para indicar qué cambios has hecho.

## Ver el Historial de Commits
```bash
git log
```
Este comando muestra un historial de commits en el repositorio, incluyendo detalles como identificadores, autores, fechas y mensajes de commit.
