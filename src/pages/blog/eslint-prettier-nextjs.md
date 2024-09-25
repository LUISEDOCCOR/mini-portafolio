---
layout: ../../layouts/Blog.astro
title: ¿Cómo configurar correctamente ESLint y prettier en un proyecto de next JS?
desc: Configura ESLint y Prettier en Next.js para garantizar un código limpio y consistente, mejorando la calidad y mantenibilidad del proyecto.
date: 22/09/2024
image_path: /og/eslint-prettier.webp
---
En este artículo, aprenderás a configurar ESLint y Prettier en tu proyecto de Next.js. Estas herramientas son fundamentales para mantener un código limpio y coherente, facilitando la colaboración en equipo y mejorando la calidad del software. ESLint se encarga de analizar tu código y detectar errores o prácticas no recomendadas, mientras que Prettier se ocupa de formatear el código automáticamente según convenciones predefinidas. Juntos, ayudan a evitar problemas comunes y aseguran que tu código siga un estilo uniforme. A lo largo de esta guía, te mostraremos los pasos necesarios para integrar ambas herramientas en tu proyecto de Next.js, permitiéndote enfocarte en lo que realmente importa: desarrollar una aplicación web excepcional.

### En nuestra terminal hacemos lo siguiente 
```bash
rm -r .eslintrc.json
pnpx eslint --init
pnpm i -D eslint-plugin-prettier@4.0.0
pnpm i -D prettier prettier-plugin-tailwindcss
touch .prettierrc
```
### En el archivo *.prettierrc* añadimos lo siguiente
```json
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```
### Tu archivo de configuración de ESLint debería verse algo así (*eslint.config.mjs*)

```js
import globals from "globals";
import tseslint from "typescript-eslint";
import pluginReactConfig from "eslint-plugin-react/configs/recommended.js";
//Importamos dependencias de prettier
import prettierConfig from "eslint-config-prettier";
import prettierPlugin from "eslint-plugin-prettier";

export default [
  {files: ["**/*.{js,mjs,cjs,ts,jsx,tsx}"]},
  { languageOptions: { parserOptions: { ecmaFeatures: { jsx: true } } } },
  {languageOptions: { globals: globals.browser }},
  ...tseslint.configs.recommended,
  // Añadimos dependencias de prettier a configuración de ESLint
  prettierConfig,
  prettierPlugin,
  pluginReactConfig,{
  	//Añadimos estas reglas a la configuración
    rules: {
      ...prettierConfig.rules,
      "react/react-in-jsx-scope": "off",
      "prettier/prettier": "error "
    }
  }
];
```

### Recuerda tener las extensiones de ESLint y prettier instaladas en vscode
