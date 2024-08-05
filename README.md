# Astro-PandaCss-Tailwind_template

## Guia para integrar Panda con Tailwind (*y eventualmente si se desea con shadcn*)

1. #### Primero debes de instalar Astro
    - Desde aqui: [Astro Build](https://docs.astro.build/en/install-and-setup/#start-a-new-project)

2. #### Luego Debes de instalar Panda (sigue todo los pasos, eventualmente los modificaremos)
    -  Desde aqui: [Panda](https://panda-css.com/docs/installation/astro#install-panda)

3. #### Instala desde la documentacion de Shadcn [a Tailwind](https://ui.shadcn.com/docs/installation/astro) (dale si a todo) **PERO**, antes del paso de ```Run the shadcn-ui init command to setup your project: ...``` omitelo por ahora...

4. #### Agrega la dependencia ```sh npm i autoprefixer```

5. #### Luego revisa el directorio llamado: Panda-Tailwind_template, en este revisa primero el apartado de package.json, que luzca algo parecido

6. #### Despues en archivo ```astro.config.mjs```, remueve la integration de tailwind

```mjs
    //Ejemplo:

    import { defineConfig } from 'astro/config';
    import react from "@astrojs/react";

    // https://astro.build/config
    export default defineConfig({
        integrations: [react()]
    });
```


7. #### Eventualmente en el archivo ```postcss.config.cjs``` debe lucir algo como:
```cjs
    module.exports = {
        plugins: {
            tailwindcss: {},
            '@pandacss/dev/postcss': {},
            autoprefixer: {}
	    }
    };
```

8. #### Agrega en el archivo de ```panda.config.ts```:

```ts
	layers: {},
```


9. #### Despues modifica el archivo de ```tailwind.config.ts``` agregando esto:

```ts
	corePlugins: {
		preflight: false,
	}
```


10. #### Y finalmente el ```index.css``` en el src (**src/index.css**) debe lucir algo como esto:

```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;

    @layer reset, base, tokens, recipes, utilities;

    /* if you decide to rename layers, you can use it like below */
    /* @layer panda_reset, panda_base, panda_tokens, panda_recipes, panda_utilities; */
```