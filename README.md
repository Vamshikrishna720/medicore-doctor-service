# medicore-doctor-service

Doctor profile & search service for the **MediCore** healthcare platform
([monorepo](https://github.com/Vamshikrishna720/medicore)).

## Highlights

- **Public doctor search** (no login): filter by specialization (indexed), min experience, max fee — paginated
- **On/off-duty toggle** (`available`) — separate from account deactivation; off-duty doctors vanish from search instantly
- Availability window (`availableFrom`/`availableTo`) consumed by appointment-service to validate 30-minute slots
- `/internal/doctors/{id}` + `/internal/doctors/by-user/{userId}` Feign endpoints

## Endpoints (via gateway, `/api`)

| Method | Path | Access |
|---|---|---|
| GET | `/doctors?specialization=&minExperience=&maxFee=&page=` | public |
| GET | `/doctors/{id}`, `/doctors/specializations` | public |
| POST/GET/PUT | `/doctors/me` | DOCTOR |
| PATCH | `/doctors/me/availability?available=` | DOCTOR |
| GET | `/internal/doctors/**` | internal token |

## Run

> **Prerequisite:** this repo depends on `com.medicore:medicore-common:1.0.0`. Install it to your local Maven repo first — clone [medicore-common](https://github.com/Vamshikrishna720/medicore-common) and run `mvn clean install` there. CI has the same requirement (publishing common to GitHub Packages would make this repo fully self-contained).

```bash
mvn spring-boot:run          # :8083 (needs MySQL + Eureka)
```

Swagger: `http://localhost:8083/swagger-ui/index.html`
