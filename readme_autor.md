# matter-autor

Matter-autor genera un bloque de autoría y transparencia que muestra información sobre la fecha de actualización, responsables de contenido y enlaces relacionados. Forma parte del catálogo corporativo de Web Components de la Junta de Andalucía.

## Instalación y servidor de desarrollo

Para levantar el web component en local, se deberá seguir una serie de pasos en el orden correcto, ya que si no, no se podrá iniciar correctamente. Los pasos que se deben seguir son los siguientes:

1. Eliminar el fichero `.npmrc` para así eliminar los repositorios y usuarios almacenados y actualizarlos con los datos necesarios correctos.
    ```bash
    rm C:\Users\{{USER}}\.npmrc
    ```

2. Acceder al [repositorio de web-components del MSD](https://gitlab.juntadeandalucia.es/pt-exp-webcomponents) y seleccionar el que se necesite.  
3. Clicar en el botón **"Clone"** y copiar el enlace HTTPS.  
4. En local, posicionarse en la carpeta donde se quiera descargar el web-component y abrir una consola de comandos. A continuación, ejecutar el siguiente comando:
    ```bash
    git clone {{enlace HTTPS copiado}}
    ```
    Tras la ejecución de este comando, se habrá creado la carpeta del proyecto `matter-autor`.
5. Configurar el registro privado de los componentes corporativos:
    ```bash
    npm config set @matter:registry=https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/
    ```
6. Instalar las dependencias del web component:
    ```bash
    npm i
    ```
7. Levantar el proyecto con el servidor de desarrollo de webpack:
    ```bash
    npm start
    ```
8. El proyecto se podrá visualizar en tiempo real en la siguiente ruta:  
   [http://localhost:3000/](http://localhost:3000/)

---

## Uso

Para hacer uso de este web-component se deberán realizar dos sencillos pasos:

1. Importar el compilado del web-component en el proyecto actual:
    ```bash
    import '@matter/matter-autor/dist/matter-autor';
    ```
2. Llamar a dicho web-component desde el fichero `.html` donde se quiera mostrar:
    ```html
    <matter-autor></matter-autor>
    ```

---

## Ejemplos de uso

### Autoría con un solo bloque
```html
<matter-autor
  stylesheetversion="latest"
  idelement="autoria-id"
  fecha="12 agosto de 2023"
  historialurl="https://ejemplo.com/historial"
  sections='[
    {
      "title": "Transparencia del organismo",
      "description": "Esta página contiene información actualizada sobre la transparencia y los responsables institucionales del organismo.",
      "items": [
        {
          "icon": "fa-user",
          "texto": "Responsable de la información publicada:",
          "linkText": "Junta de Andalucía",
          "linkUrl": "https://www.juntadeandalucia.es"
        }
      ]
    }
  ]'>
</matter-autor>
```

---

### Autoría con varios bloques
```html
<matter-autor
  stylesheetversion="latest"
  idelement="autoria-id"
  fecha="12 agosto de 2023"
  historialurl="https://ejemplo.com/historial"
  sections='[
    {
      "title": "Transparencia del organismo",
      "description": "Esta página contiene información actualizada sobre la transparencia y los responsables institucionales del organismo.",
      "items": [
        {
          "icon": "fa-user",
          "texto": "Responsable de la información publicada:",
          "linkText": "Junta de Andalucía",
          "linkUrl": "https://www.juntadeandalucia.es"
        }
      ]
    },
    {
      "title": "Participación ciudadana",
      "description": "Información sobre los mecanismos de participación y acceso a datos.",
      "items": [
        {
          "icon": "fa-user",
          "texto": "Responsable del contenido:",
          "linkText": "Consejería de Participación",
          "linkUrl": "https://participacion.juntadeandalucia.es"
        }
      ]
    }
  ]'>
</matter-autor>
```

---

### Autoría con datos cargados desde un endpoint externo
```html
<matter-autor
  stylesheetversion="latest"
  idelement="autoria-id"
  fecha="12 agosto de 2023"
  historialurl="https://ejemplo.com/historial"
  endpointurl="https://juntadeandalucia.es/ssdigitales/festa/storybook/matter-autor-1.2.0.json">
</matter-autor>
```

---

## Props

| Prop               | Tipo     | Descripción                                                                                   |
| :----------------- | :------- | :-------------------------------------------------------------------------------------------- |
| `stylesheetVersion` | string   | Versión de la hoja de estilos a usar. Por defecto `"latest"`.                                |
| `idElement`         | string   | Identificador del bloque principal de autoría.                                               |
| `historialUrl`      | string   | URL al historial de cambios o versiones anteriores del contenido.                            |
| `fecha`             | string   | Fecha de la última actualización mostrada en el bloque de autoría.                          |
| `endpointURL`       | string   | URL de un JSON externo desde el que cargar los datos de autoría dinámicamente.              |
| `sections`          | array    | Estructura de datos en formato JSON con las secciones, descripciones e ítems de autoría.     |

---

## Producción

### **Publicación del web-component en NEXUS PRO**
👉 [https://nexus.paas.junta-andalucia.es/](https://nexus.paas.junta-andalucia.es/)

1. Eliminar `.npmrc`:
    ```bash
    rm C:\Users\{{USER}}\.npmrc
    ```
2. Actualizar la versión en `package.json`.  
3. Instalar dependencias:
    ```bash
    npm i
    ```
4. Incluir en `package.json` las siguientes líneas:
    ```json
    "files": [
      "dist"
    ]
    ```
5. Generar el compilado:
    ```bash
    npm run build
    ```
6. Configurar el registro:
    ```bash
    npm config set registry https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/
    npm config set @matter:registry=https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/
    ```
7. Autenticarse con el usuario correspondiente:
    ```bash
    npm adduser --registry=https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/ --always-auth
    ```
8. Publicar la nueva versión:
    ```bash
    npm publish
    ```
