# Guía de Pruebas para El Chato Sonora

## 1. Pruebas Locales (Desarrollo)

### Funcionalidades a Probar:

#### A. Máquina de la Suerte ✅
- Abrir desde botones del header (desktop y mobile)
- Abrir desde botón principal
- Generar números aleatorios (1-50 boletos)
- Verificar animaciones y transiciones
- Continuar al checkout con números seleccionados

#### B. Grilla de Boletos
- Cargar grilla de 1000 boletos
- Seleccionar boletos individuales
- Verificar estados: disponible (verde), reservado (amarillo), vendido (rojo)
- Continuar al checkout con boletos seleccionados

#### C. Verificador de Boletos
- Buscar por número de boleto
- Buscar por teléfono del cliente
- Verificar información mostrada según estado
- Protección de privacidad (datos ocultos para no pagados)

#### D. Proceso de Checkout
- Formulario de datos del cliente
- Validación de campos requeridos
- Simulación de pago
- Generación de boleto digital

#### E. Panel de Administración (/admin)
- Estadísticas en tiempo real
- Configuración de sorteo
- Recordatorios por WhatsApp (simulado)

## 2. Datos de Prueba Preconfigurados

### Base de Datos Seeded:
```
- 1000 boletos disponibles
- 97 boletos vendidos (números bajos)
- 59 boletos reservados
- 844 boletos disponibles
- 1 sorteo activo: Toyota Tacoma 2025
```

### Boletos de Prueba:
- **Boleto #26**: Vendido - Cliente: Juan Pérez, Tel: 5551234567
- **Boleto #4**: Disponible
- **Números bajos (1-97)**: Mayoría vendidos
- **Números altos (98-1000)**: Mayoría disponibles

## 3. Pruebas de Interfaz

### Responsive Design:
- Desktop (1920x1080)
- Tablet (768x1024)
- Mobile (375x667)
- Verificar menú hamburguesa en mobile

### Navegación:
- Links del header funcionando
- Scroll suave a secciones
- Modal system (solo un modal abierto a la vez)

### Temas:
- Modo claro y oscuro
- Colores brand consistentes (verde #22c55e)

## 4. Pruebas de API

### Endpoints Disponibles:
```
GET /api/raffle - Información del sorteo
GET /api/stats - Estadísticas en tiempo real
GET /api/tickets - Lista de boletos (admin)
GET /api/tickets/verify/:identifier - Verificar boleto
POST /api/tickets/random - Generar números aleatorios
POST /api/tickets/reserve - Reservar boletos
```

### Pruebas con curl:
```bash
# Generar números aleatorios
curl -X POST http://localhost:5000/api/tickets/random \
  -H "Content-Type: application/json" \
  -d '{"count": 3}'

# Verificar boleto
curl http://localhost:5000/api/tickets/verify/26

# Obtener estadísticas
curl http://localhost:5000/api/stats
```

## 5. Lista de Verificación Final

### Funcionalidad Core:
- [ ] Máquina de la suerte genera números correctamente
- [ ] Grilla de boletos carga y muestra estados
- [ ] Verificador encuentra boletos por número/teléfono
- [ ] Checkout procesa datos correctamente
- [ ] Boleto digital se genera después del pago
- [ ] Panel admin muestra estadísticas

### Interfaz de Usuario:
- [ ] Todos los botones funcionan
- [ ] Modales abren y cierran correctamente
- [ ] No hay errores de consola
- [ ] Responsive en todos los tamaños
- [ ] Animaciones suaves
- [ ] Textos en español

### Datos y Seguridad:
- [ ] Base de datos persiste entre reinicios
- [ ] Información sensible protegida
- [ ] Validación de formularios funciona
- [ ] Estados de boletos se actualizan

## 6. Preparación para Producción

### Antes de Publicar:
1. **Configurar Base de Datos Real**: Reemplazar datos seed con datos reales
2. **Integrar Pagos Reales**: Conectar con Stripe/PayPal
3. **WhatsApp Real**: Configurar API de WhatsApp Business
4. **Dominio Personalizado**: Configurar en Replit
5. **Backup de Datos**: Configurar respaldos automáticos
6. **Monitoreo**: Configurar alertas de errores

### Variables de Entorno Necesarias:
```
STRIPE_SECRET_KEY=sk_live_...
TWILIO_ACCOUNT_SID=AC...
TWILIO_AUTH_TOKEN=...
TWILIO_PHONE_NUMBER=+1...
```

## 7. Métricas de Rendimiento

### Tiempos de Respuesta Esperados:
- Carga inicial: < 3 segundos
- Generación de números: < 500ms
- Búsqueda de boletos: < 200ms
- Estadísticas: < 300ms

### Capacidad:
- Usuarios simultáneos: 100+
- Boletos por sorteo: 1000-10000
- Transacciones por minuto: 50+

¡Tu sistema está funcionando correctamente y listo para pruebas exhaustivas!