# Team Management System (TMS)

A Node.js web application for managing team players, sessions, and attendance using Supabase as the database.

## Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Set up your Supabase project:
   - Create a new project at [supabase.com](https://supabase.com)
   - Go to Settings > API to get your project URL and anon key

3. Configure environment variables:
   - Copy `.env.example` to `.env`
   - Update the `.env` file with your actual Supabase credentials:
     ```
     SUPABASE_URL=https://your-project-ref.supabase.co
     SUPABASE_ANON_KEY=your_actual_anon_key_from_supabase_dashboard
     ```

4. Start the server:
   ```bash
   npm start
   # or
   node server.js
   ```

## Security Note

⚠️ **Never commit your `.env` file to version control!** It contains sensitive API keys. The `.gitignore` file is configured to automatically exclude it.

## Features

- Player management (CRUD operations)
- Session scheduling
- Attendance tracking
- Responsive mobile-friendly interface
- User authentication
   Get the anon key from your Supabase dashboard: Settings > API > Project API keys > anon public

4. Create the following tables in your Supabase database (SQL Editor):

   **players** table:
   ```sql
   CREATE TABLE players (
     id SERIAL PRIMARY KEY,
     name TEXT NOT NULL,
     position TEXT,
     phone TEXT
   );
   ```

   **sessions** table:
   ```sql
   CREATE TABLE sessions (
     id SERIAL PRIMARY KEY,
     date DATE NOT NULL,
     time TIME WITHOUT TIME ZONE NOT NULL,
     location TEXT NOT NULL,
     players_count INTEGER
   );
   ```

   **attendance** table:
   ```sql
   CREATE TABLE attendance (
     id SERIAL PRIMARY KEY,
     player_id INTEGER NOT NULL,
     session_id INTEGER NOT NULL,
     present BOOLEAN DEFAULT false,
     FOREIGN KEY (player_id) REFERENCES players(id),
     FOREIGN KEY (session_id) REFERENCES sessions(id)
   );
   ```

   **users** table:
   ```sql
   CREATE TABLE users (
     id SERIAL PRIMARY KEY,
     username TEXT NOT NULL UNIQUE,
     password TEXT NOT NULL,
     role TEXT DEFAULT 'coach',
     email TEXT UNIQUE
   );
   ```

## Running the Application

Start the development server:
```bash
npm run dev
```

Or start the production server:
```bash
npm start
```

The server will run on http://localhost:3000

## API Endpoints

### Players
- `GET /api/players` - Get all players
- `POST /api/players` - Create a new player
- `PUT /api/players/:id` - Update a player
- `DELETE /api/players/:id` - Delete a player

### Sessions
- `GET /api/sessions` - Get all sessions
- `POST /api/sessions` - Create a new session
- `PUT /api/sessions/:id` - Update a session
- `DELETE /api/sessions/:id` - Delete a session

### Attendance
- `GET /api/attendance` - Get all attendance records
- `POST /api/attendance` - Create a new attendance record
- `PUT /api/attendance/:id` - Update an attendance record
- `DELETE /api/attendance/:id` - Delete an attendance record

## Frontend

The HTML files in the `public/` directory can be accessed directly and will make API calls to these endpoints. You'll need to add JavaScript to the HTML files to interact with the API.