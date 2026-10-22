# Architecture (target, not implemented)

```mermaid
flowchart TD
  U[User browser] --> N[Next.js frontend]
  N -->|HTTPS multipart + job token| F[FastAPI API]
  F --> P[(PostgreSQL job metadata)]
  F --> S[Private temporary audio storage]
  F --> W[Bounded local inference worker]
  W --> M[Speech enhancement model]
  W --> S
  W --> P
  N -->|poll status + download| F
```

## Monorepo target
```
nirava/
  frontend/
    src/app/{layout.tsx,page.tsx,globals.css}
    src/components/{audio,layout,ui}/
    src/hooks/useEnhancementJob.ts
    src/lib/api.ts
    src/types/audio.ts
    public/
    package.json
  backend/
    app/main.py
    app/api/v1/{health.py,enhancement.py}
    app/core/{config.py,security.py}
    app/db/{session.py,models.py}
    app/schemas/enhancement.py
    app/services/{audio.py,enhancer.py,storage.py,model_loader.py,job_runner.py}
    alembic/versions/
    tests/
    pyproject.toml
  infra/compose.yaml
  docs/
  scripts/
  AGENTS.md
  README.md
  .gitignore
  .env.example
```

## Execution
- Satu FastAPI instance dengan worker inference terbatasi untuk demo; PostgreSQL menjaga status tetapi tidak menjalankan pekerjaan.
- Hindari pemrosesan berat langsung pada request thread. Job yang terputus saat restart harus dipulihkan atau ditandai gagal saat startup.
- Model dimuat sekali per worker. Atur konkurensi sesuai CPU/GPU.
- Penyimpanan file privat di luar web root, direktori runtime tidak masuk Git.
- Di deployment multi-instance, gunakan object storage + durable queue; jangan anggap filesystem lokal bersama.
- Validasi codec dengan decoder, batasi ukuran dan durasi, terapkan timeout.

## Trade-off
PostgreSQL lebih berat daripada SQLite untuk MVP tetapi dipilih untuk deployment persisten dan pembelajaran skema. Next.js lebih fleksibel untuk desain daripada Streamlit tetapi menambah kompleksitas TypeScript.
