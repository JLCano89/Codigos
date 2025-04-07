# README

Streamlit + Ngrok en Google Colab (Guía paso a paso)

Este proyecto muestra cómo ejecutar una aplicación de Streamlit directamente desde Google Colab, utilizando Ngrok para obtener una URL pública y acceder a la interfaz de la app desde cualquier navegador.

Herramientas utilizadas
- Streamlit: Framework para crear aplicaciones web interactivas en Python.
- Ngrok: Servicio para exponer puertos locales a Internet de forma segura.
- Google Colab: Entorno de notebooks basado en la nube de Google.

Archivos del proyecto
/MiProyecto/
├── app.py          # Código principal de la app de Streamlit
├── notebook.ipynb  # Notebook de Google Colab con el código para correr Ngrok
└── README.txt      # Este documento

Requisitos
Antes de empezar, asegúrate de que tienes:
- Una cuenta de Google para acceder a Google Colab.
- Un archivo llamado app.py que contenga tu aplicación de Streamlit (puedes copiar el ejemplo básico más abajo).

Instrucciones paso a paso

1. Subir tu archivo app.py a Colab
- Abre tu notebook en Google Colab.
- Sube tu archivo app.py desde el menú: Archivos > Subir

Si no tienes un archivo app.py, puedes crear uno con el siguiente ejemplo:

    import streamlit as st
    st.title("Hola desde Streamlit en Colab ")
    st.write("¡Esta es una app de prueba corriendo con Ngrok!")

2. Copia este código en una celda de Colab y ejecútalo

    !pip install -q pyngrok streamlit

    from pyngrok import ngrok
    import os
    import threading

    ngrok.kill()
    port = 8501

    def run():
        os.system(f"streamlit run app.py --server.port {port}")

    threading.Thread(target=run).start()
    public_url = ngrok.connect(port)
    print(f" Tu aplicación Streamlit está disponible aquí: {public_url}")

3. Ver la aplicación en línea
Después de ejecutar la celda, aparecerá una URL como:
     Tu aplicación Streamlit está disponible aquí: http://xxxxxx.ngrok.io

Haz clic o copia esa dirección en tu navegador y verás tu app funcionando.

 Cierre y solución de errores comunes
- Si obtienes un error como ERR_NGROK_108, significa que tienes otra sesión de ngrok abierta.
  Solución: Ejecuta ngrok.kill() antes de abrir un nuevo túnel.
- Si haces cambios en app.py, reinicia el entorno o vuelve a ejecutar las celdas.

 Prueba rápida (código de ejemplo para app.py)

    import streamlit as st
    import datetime

    st.title("Demo Interactiva")
    nombre = st.text_input("¿Cuál es tu nombre?")
    if nombre:
        st.success(f"Hola, {nombre} ")
        
    fecha = st.date_input("Selecciona una fecha")
    st.write("Fecha seleccionada:", fecha)
    st.write("Fecha y hora actual:", datetime.datetime.now())

 Recursos adicionales
- Documentación oficial de Streamlit: https://docs.streamlit.io/
- Documentación de Ngrok: https://ngrok.com/docs
- Guía de uso de Google Colab: https://research.google.com/colaboratory/faq.html

Este proyecto fue configurado para facilitar la ejecución de aplicaciones web simples en entornos de notebooks, sin necesidad de servidores externos.
