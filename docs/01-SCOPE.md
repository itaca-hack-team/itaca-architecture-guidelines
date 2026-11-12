# 01 - Alcance del Producto (MVP Scope)

## 1. Problema de Negocio
Los espacios de coworking y salas de reunión en Piura gestionan sus reservas manualmente por WhatsApp y hojas de cálculo, generando cruces de horarios y demoras en la confirmación.

## 2. Objetivo del MVP
Permitir que un usuario consulte disponibilidad en tiempo real y reserve una sala en menos de 60 segundos, registrando la solicitud en base de datos sin intervención manual.

## 3. Core Loop (Flujos Críticos Incluidos en el MVP)
1. **Consultar Salas y Disponibilidad:** Listar salas activas y ver bloques horarios ocupados para una fecha específica.
2. **Crear Reserva:** Seleccionar sala, fecha, hora de inicio/fin y datos básicos del solicitante, validando que no exista traslape de horario.
3. **Consultar Estado de Reserva:** Obtener el detalle y código de confirmación de una reserva creada mediante su ID.

## 4. OUT OF SCOPE (Explícitamente FUERA del MVP)
> **Instrucción para la IA:** NO implementar, sugerir ni crear estructura para ninguno de los siguientes puntos:
- [ ] Pasarela de pagos en línea (Culqi / Niubiz / tarjetas).
- [ ] Sistema de registro de usuarios, login con contraseña o roles avanzados (RBAC).
- [ ] Panel administrativo con gráficos de analítica o exportación a Excel/PDF.
- [ ] Envío automático de correos electrónicos o notificaciones por WhatsApp.
- [ ] Cancelación o reprogramación automatizada por el usuario final.
