# Runbook — Push Databricks code to GitHub (new UI)

Goal

Connect Databricks to GitHub, work inside a Git folder (/Repos), then Commit & Push your notebooks.

## 0) Requirements

- You have write access to the target GitHub repo (e.g., `<your-git-user-account>/eurostyle-contonso-ma-unified-data-ai-databricks-fabric-sol`) or to your fork.
- In your Databricks workspace, Repos (Git folders) and GitHub provider are enabled. If you don't see Repos or Linked accounts, ask a workspace admin to enable them.

## 1) Create a GitHub Personal Access Token (PAT)

1. On GitHub (signed in with the account that will push), go to Profile → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token.

![picture 0](../../images/dc627375f53cdbbd973c77d3368b1482ecbd752b85124d896d45a39d4b043450.png)  

![picture 1](../../images/906f832fba17addabcc95ebac21cb85d5308a79ad14bf4ce627ddf24e26a0b0f.png)  


2. Repository access: Only select repositories → select your repo.
3. Permissions (Repository permissions): set Contents: Read and write. (Optional: Pull requests: Read.)
4. Choose a name and expiration → Generate token → copy the token.
   
![picture 2](../../images/b6bedb7750e707b3186c0d26b3ba009516e0d9dd6b603b146e8112ef3471c7ab.png)  

![picture 3](../../images/6dc84d8bcfcc6d229e501dc70cf1c9ca1eadd5413ccddd697de4cbf1177fcd8b.png)  

![picture 4](../../images/02078cd338ff0e59e42500050a9d1a0c8863ed36d167933ae7f88c17d5f4508f.png)  



Note: A Classic token with the single repo scope also works as an alternative.

## 2) Link GitHub in Databricks

1. In Databricks: Settings → User → Linked accounts.

![picture 5](../../images/4565445d27d255f8fa7820a4538cac4667157abe968d3183f522e0d4444e9dd7.png)  

![picture 6](../../images/4a41cc1fefc4cba40f557820b3eead8e5affff4b14b252745dca06c334bb8508.png)  


2. Connect new → GitHub → paste the PAT → Save.

![picture 8](../../images/c94a1b885b2fb5bad5594f2771a974c0be9fc4a6762e56570d53115bad1db7c7.png)  

![picture 9](../../images/d8ee35482d51f2f211e4f13f3e4d97555a382dbae600e3ab5e21ae16749b5b40.png)  


3. If you have an old/incorrect entry, remove it first to avoid account mix-ups.

## 3) Clone the repo into Repos

1. Left sidebar → Repos (or Git folders) → Clone.
2. Paste the HTTPS repo URL, e.g.:

```
https://github.com/<your-git-user-account>/eurostyle-contonso-ma-unified-data-ai-databricks-fabric-sol.git
```

3. Branch: `main` → Clone.
4. You now have a path like `/Repos/<owner>/<repo>`.

Only items under `/Repos/` are under Git control. Anything under `Workspace/` is not.

## 4) Move your existing notebooks into the repo

1. In Workspace, right-click your folder (e.g., `Epic 1 – Data Foundation Platform`) → Move → target `/Repos/<owner>/<repo>/` (create a `solution/` subfolder if desired).

## 5) Commit & Push from Databricks

1. Open any file from `/Repos/...`.
2. Click the branch badge (e.g., `main`) or the Git icon to open the Changes panel.
3. Select files → Stage.
4. If prompted, Pull first.
5. Enter a commit message (e.g., `feat(epic1): initial notebooks`) → Commit & push.

Working on protected `main`?

- Create a branch (branch menu → Create branch, e.g., `feat/epic1`) → Commit & Push → open a Pull Request on GitHub.

## 6) Multiple accounts (common cases)

- Want to push to `<your-git-user-account>/...` → the PAT in Linked accounts must belong to `<your-git-user-account>`.
- Want to keep using your account → clone your fork, push there, then open a PR to the original repo.

## 7) Quick troubleshooting

- 403 "denied to <username>" → the stored PAT belongs to the wrong GitHub account.
  - Fix: In Settings → User → Linked accounts, delete the entry and add a PAT from the correct account (or push to your fork).
- No Commit/Push buttons → you're editing under `Workspace/`, not `/Repos/`. Open files from `/Repos`.
- Cannot see Repos / Linked accounts → ask an admin to enable Git folders and the GitHub provider in Workspace admin → Workspace settings.
- Databricks UI glitch (azurefd.net assets) → sign out/in, hard refresh (Ctrl+F5), try a private window, or clear site data for the workspace domain.

## 8) One-minute checklist

- [ ] PAT created on the right GitHub account with Contents: Read & write
- [ ] PAT saved in Databricks → Settings → User → Linked accounts → GitHub
- [ ] Repo cloned under `/Repos` (not `Workspace`)
- [ ] Notebooks moved into `/Repos/...`
- [ ] Stage → Commit → Push (or branch → PR)

## Tips

- Add a short entry in the repo root `README.md` linking to the runbook so contributors can find it quickly.
- If your organization uses an internal docs site, mirror the runbook there and include the repo link.
- For sensitive organizations: store PATs in a secure secret store—never commit them.

---

File created: `docs/runbooks/push-databricks-to-github.md`
