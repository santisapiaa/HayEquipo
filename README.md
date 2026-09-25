> **Nota:** este repositorio es una versión propia del proyecto grupal **HayEquipo**
> ([ivolevy/hayequipo-mvp](https://github.com/ivolevy/hayequipo-mvp)), desarrollado en
> equipo para la facultad. Mi rol en el equipo: **diseño de la interfaz y frontend**.

# HayEquipo

Plataforma de gestión centralizada para planteles amateurs de fútbol. Permite a un
Director Técnico organizar partidos, convocatorias y formaciones, mientras que
Preparador Físico y Nutricionista hacen seguimiento del estado de los jugadores, y
cada jugador ve su propia información desde su perfil.

## Roles

- **DT (Director Técnico):** crea partidos, arma convocatorias y formaciones, gestiona
  el plantel y publica avisos.
- **Jugador:** confirma/rechaza convocatorias, ve entrenamientos y plan nutricional.
- **PF (Preparador Físico):** hace seguimiento del estado físico del plantel y arma
  planes de entrenamiento.
- **Nutricionista:** define objetivos y recomendaciones nutricionales para el equipo.
- **Admin:** gestión general del equipo y planes.

## Tecnologías

- [Vite](https://vitejs.dev/) + [React](https://react.dev/) + [TypeScript](https://www.typescriptlang.org/)
- [shadcn-ui](https://ui.shadcn.com/) + [Tailwind CSS](https://tailwindcss.com/)
- [Supabase](https://supabase.com/) (base de datos, autenticación y realtime)
- PWA (instalable, con soporte offline básico vía service worker)

## Desarrollo local

### 1. Requisitos

- Node.js 18+
- Un proyecto de [Supabase](https://supabase.com/) propio (gratis)

### 2. Instalar dependencias

```sh
npm install
```

### 3. Configurar variables de entorno

Creá un archivo `.env` en la raíz del proyecto:

```sh
VITE_SUPABASE_URL=https://tu-proyecto.supabase.co
VITE_SUPABASE_ANON_KEY=tu_anon_key
```

Estas credenciales se obtienen desde el dashboard de Supabase, botón **Connect** o
**Project Settings → API Keys**. Nunca subas este archivo al repo (ya está en
`.gitignore`), y nunca uses la `service_role` key en el frontend.

### 4. Base de datos

Las migraciones SQL están en [`supabase/migrations/`](supabase/migrations/). Corré cada
una en el **SQL Editor** de tu proyecto de Supabase, en este orden:

1. `20260518111023_hayequipo_tables.sql`
2. `20260603150000_multiteam_schema.sql`
3. `20260622000000_fix_constraints_and_persistence.sql`
4. `20260622010000_add_team_plan.sql`
5. `20260622020000_add_push_subscriptions.sql`
6. `grants.sql`
7. `fix_access.sql`
8. `policies.sql`

(`restored_migration.sql` es un backup de la migración 1, no hace falta correrlo.)

### 5. Levantar el servidor

```sh
npm run dev
```

La app queda disponible en `http://localhost:8080`.

## Scripts disponibles

| Comando | Descripción |
|---|---|
| `npm run dev` | Servidor de desarrollo |
| `npm run build` | Build de producción |
| `npm run lint` | Linter (ESLint) |
| `npm run test` | Tests (Vitest) |

## Deploy

El proyecto está pensado para desplegarse en [Vercel](https://vercel.com/): importá el
repo y configurá las mismas dos variables de entorno (`VITE_SUPABASE_URL` y
`VITE_SUPABASE_ANON_KEY`) en Project Settings → Environment Variables.
