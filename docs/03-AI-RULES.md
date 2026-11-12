# 04 - Directrices y Reglas para el Agente de IA

Estas instrucciones gobiernan la generación de código en este repositorio.

## 1. Convenciones de Código
- **Idioma:** Todo el código (nombres de variables, funciones, clases, archivos y endpoints) debe escribirse en **inglés**. Los mensajes de error orientados al usuario y comentarios de negocio pueden ir en **español**.
- **Tipado Estricto:** Prohibido usar `any` en TypeScript. Usar siempre las interfaces definidas en `docs/03-API-CONTRACT.md`.
- **Arquitectura Modular (NestJS):** Separar estrictamente `controller` (rutas y HTTP), `service` (lógica de negocio y validación de traslapes) y `dto` (validación de entrada).

## 2. Manejo de Errores
- Usar las excepciones nativas de NestJS (`BadRequestException`, `NotFoundException`, `ConflictException`).
- Nunca devolver errores genéricos `500` para reglas de negocio incumplidas.

## 3. Restricciones Negativas (PROHIBICIONES)
1. **NO instalar dependencias externas** (`npm install`) sin autorización explícita en el prompt.
2. **NO inventar endpoints o campos** que no existan en `docs/03-API-CONTRACT.md`.
3. **NO crear datos mockeados (hardcoded)** dentro de los servicios; conectar directamente con la instancia de Firestore configurada en `src/config/`.
4. **NO implementar funcionalidades listadas en `OUT OF SCOPE`** dentro de `docs/01-SCOPE.md`.
5. **NO modificar la estructura de carpetas** definida en `docs/02-ARCHITECTURE.md`.
