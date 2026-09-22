# Windows RDP su GitHub Actions

Avvia una VM Windows (`windows-latest`) con RDP abilitato, raggiungibile
in modo sicuro tramite la tua rete Tailscale.

## Setup (una tantum)

Nel repo vai su **Settings → Secrets and variables → Actions → New repository secret**
e crea questi due secret:

| Secret | Valore |
|---|---|
| `RDP_PASSWORD` | la password che userai per collegarti in RDP (utente `rdpuser`) |
| `TAILSCALE_AUTHKEY` | una auth key di Tailscale (generala su https://login.tailscale.com/admin/settings/keys — spunta **Reusable** ed **Ephemeral**, taggala come vuoi) |

## Uso

1. Vai su **Actions → Windows RDP → Run workflow → Run workflow**
2. Aspetta che il job arrivi allo step "Connect to Tailscale"
3. Nei log dello step trovi l'indirizzo, tipo:
   ```
   RDP address: 100.x.x.x
   ```
4. Collegati con `mstsc /v:100.x.x.x`, utente `rdpuser`, password del secret

La VM resta attiva fino a ~5h50m (limite dei runner GitHub), poi si spegne.
Per una nuova sessione riesegui il workflow.

## Note

- La VM entra nella **tua** tailnet: niente IP pubblici, niente porte esposte.
- GitHub può sospendere repo/account per uso RDP sui runner: usalo con criterio.
