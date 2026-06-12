# n8n AI Workflow Automation System

This directory contains a complete AI-powered workflow automation system built with n8n. The system handles customer messages, classifies intent, uses a RAG (Retrieval-Augmented Generation) agent for property inquiries, and updates a Google Sheets dashboard for analytics.

## Workflows Included:

*   `reto-final-main.json`: The main entry point that receives messages from WhatsApp, normalizes data, and delegates to specific agents using an LLM supervisor.
    ```mermaid
    graph TD
        A[WhatsApp Trigger] --> B(Normalizar_mensaje)
        B --> C[(Verificar_cliente)]
        C --> D{Existe?}
        D -- No --> E[(Registrar_cliente)]
        E --> F
        D -- Si --> F[Merge]
        F --> G[(Recuperar_historial)]
        G --> H(Formatear_historial)
        H --> I[LLM Supervisor Groq/Gemini]
        I --> J(Parsear_supervisor)
        J --> K{Switch Agente}
        
        K -- RAG --> L[Ejecutar_Agente_RAG]
        K -- CLASIFICADOR --> M[Ejecutar_Agente_Clasificador]
        K -- SALUDO --> N(Mensaje_de_Saludo)
        
        L --> O[Merge]
        M --> O
        N --> O
        
        O --> P[(Guardar_historial)]
        P --> Q[(Insertar_ticket)]
        Q --> R[(Leer_precios)]
        R --> S(Calcular_costo)
        S --> T[Enviar_mensaje WhatsApp]
    ```

*   `agente-rag.json`: A specialized RAG agent that answers real estate inquiries using a vector store (Pinecone) and documents (PDFs).
    ```mermaid
    graph TD
        A[Trigger_by_Main_Workflow] --> B(Embeddings Openrouter)
        B --> C(Parsear_embedding)
        C --> D[(Buscar_documentos Supabase)]
        D --> E(Formatear_contexto)
        E --> F[LLM Chain RAG Groq/Gemini]
        F --> G(Formatear_respuesta_RAG)
    ```

*   `agente-clasificador.json`: Handles complaints, urgent requests, and negative sentiment messages.
    ```mermaid
    graph TD
        A[Trigger_by_Main_Workflow] --> B[LLM Classifier Chain]
        B --> C(Parsear Classifier)
        C --> D{If Escalado?}
        
        D -- True --> E[Enviar_mensaje_tecnico WhatsApp]
        E --> F(Formato_mensaje_cliente)
        F --> G[Merge]
        
        D -- False --> H(Formato_mensaje_sin_escalar)
        H --> G
    ```

*   `dashboard-sheets.json`: Extracts metrics from Supabase and updates a Google Sheets dashboard for business analytics.
    ```mermaid
    graph LR
        A[Schedule Trigger] --> B[(Obtener_info_ticket Supabase)]
        B --> C[Clear sheet Google Sheets]
        C --> D[Append row Google Sheets]
    ```

*   `subir-pdf.json`: An administrative workflow to upload PDF documents to the vector store.
    ```mermaid
    graph TD
        A[Form Submission: PDF Upload] --> B[(Revisar_doc_repetido)]
        B --> C[(Borrar_chunks_repetidos)]
        C --> D[(Borrar_documento_repetido)]
        D --> E(Recuperar_binario)
        E --> F{Switch}
        F --> G[Extract text from File]
        G --> H[Merge]
        H --> I[(Insertar nuevo documento)]
        I --> J(Chunking)
        J --> K(Embeddings Openrouter)
        K --> L(Formatear_pre_insert)
        L --> M[(Insertar_embeddings Supabase)]
    ```

*   `manejo-errores.json`: A global error handling workflow to log failures and notify administrators.
    ```mermaid
    graph TD
        A[Error Trigger] --> B[LLM Chain: Translate Error]
        B --> C(Parsear_mensaje_de_error)
        C --> D[Enviar_mensaje_cliente WhatsApp]
        D --> E[Enviar_mensaje_tecnico WhatsApp]
        E --> F[(Metricas_error Supabase)]
    ```

*   `actualizar-tokens.json`: A scheduled workflow to update AI model token pricing.
    ```mermaid
    graph LR
        A[Schedule Trigger] --> B(Fetch Openrouter Models API)
        B --> C(Clasificar_modelos)
        C --> D[(Insertar_precios Supabase)]
    ```

## Note on Credentials
All sensitive credentials, API keys, and phone numbers have been redacted (`YOUR_API_KEY`, `YOUR_WEBHOOK_ID`, etc.) for security. To import these workflows into your n8n instance, you must configure the corresponding credentials in your environment.

## Screenshots
![Workflow Overview](./screenshots/workflow-overview.jpg)
