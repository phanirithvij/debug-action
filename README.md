https://github.com/phanirithvij/debug-action

GHA backed nix binary cache

This workflow does something weird and crazy
- It exposes nix store via nix-serve in a cloudflare tunnel
-- * Then one can use that url as a substitutor
-- * This can be extended to build anything in gha and retain it in gha cache
- Why not use cachix? good question, maybe because it is not oss
    - is gha oss? no but offers 10GB per cache/repo
    - so each repo is a cache
    - uptime is zero
    - github action must be running and substitutors are temporary
    - can start wf from cli when needed I guess
    - cloudflare tunnels needs own domain to work to fix the subsitutor being temporary thing
    - keys generated can be stored in repo encrypted (age or sops or something)

- Also caches nix store in github actions cache
- gha cache limits 10GB per repo

## TODO
### other whacky ideas
- push to a list of minio backed private attic servers
  without exposing their endpoints (github secrets)
- seems like attic is not required, detsys magic cache runs a server it can be used
  so, attic need not be run. But this is at the mercy of github and detsys
- never mind, attic or something is required, because magic-cache doesn't sign packages
  and public key is not known
- so running a nix-serve with temporary private/public keypair
