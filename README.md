# Ranking Villa de Getafe 26/27

Liga de pádel por parejas del Club Villa de Getafe (30 parejas, 10 divisiones de 3).
Cada mes: máx. 2 partidos por pareja, solo contra rivales de la misma división.
El admin cierra el mes a mano: 1º sube, 3º baja, 2º se mantiene (desempate: diferencia de juegos).

## PUESTA EN MARCHA (sin saber programar)

### Paso 1 — Crear la base de datos (gratis, ~5 min)
1. Entra en https://supabase.com, crea una cuenta y pulsa **New project** (ponle un nombre y una contraseña; guárdala).
2. Cuando termine de crearse, abre **SQL Editor** > **New query**.
3. Abre el archivo `supabase/setup.sql`, copia TODO su contenido, pégalo y pulsa **Run**.
   Esto crea las tablas, el código de torneo y 30 parejas de prueba.
4. Ve a **Project Settings > API** y copia dos cosas: **Project URL** y la clave **anon public**.

### Paso 2 — Publicar la web (gratis, ~10 min)
1. Crea una cuenta en https://github.com, crea un repositorio nuevo y sube todo el contenido de esta carpeta
   (botón "Add file > Upload files"). NO subas ningún archivo `.env`.
2. Crea una cuenta en https://vercel.com (entra con GitHub) > **Add New > Project** > elige tu repositorio.
3. Antes de pulsar Deploy, abre **Environment Variables** y añade:
   - `VITE_SUPABASE_URL` = el Project URL del paso 1
   - `VITE_SUPABASE_PUBLISHABLE_KEY` = la clave anon public del paso 1
4. Pulsa **Deploy**. Vercel te dará un enlace que podéis compartir con los jugadores.

## DATOS DE PRUEBA
- Código de torneo: `VG2526`
- Teléfonos de jugadores de prueba: `600000001` ... `600000060` (2 por pareja, por orden; pareja p01 = 600000001 y 600000002).
- Divisiones: p01-p03 = división 1, p04-p06 = división 2, ... p28-p30 = división 10.
- Admin: `690675116` (Niko) con código `2526`. Los admins `615867115` y `637747014` pueden entrar como admin,
  pero como jugadores solo si añadís sus teléfonos a una pareja.
- Mes activo inicial: noviembre 2026 (2026-11). Cada "Cerrar Mes" avanza al siguiente.

## AL TERMINAR LAS PRUEBAS
En `supabase/setup.sql`, al final, hay instrucciones para vaciar los datos de prueba antes de
cargar las parejas reales. Para añadir parejas reales: Supabase > **Table Editor** > tabla `pairs` > Insert row.

## SEGURIDAD (importante saber)
Esta versión conserva el funcionamiento original: los permisos de la base de datos son abiertos y los
códigos de admin viven en el código de la web. Vale para un grupo cerrado de confianza; no compartáis
el enlace públicamente. Si queréis, se puede endurecer más adelante.

## Para quien programe
`npm install` y `npm run dev` (necesita Node 18+ y un archivo `.env` copiado de `.env.example`).
Stack: React 18 + Vite + TypeScript + Tailwind + shadcn/ui + Supabase.
Cambios respecto a la versión Lovable: eliminado `lovable-tagger` y el almacenamiento de preview,
rutas con carga diferida y chunks separados (arranque más rápido), temporada 26/27 con mes inicial 2026-11.
