# pw-server — the `authd` password service

A sample server process: the IDL interfaces (`idl/`), the C++ servant, a pure-C policy library, generated stubs, a Makefile and a compile database, tests, vendored code and docs.

## Part of the agentic-orchestration-framework playground

This repo and its partner are small, self-contained samples for trying
[agentic-orchestration-framework](https://github.com/meenusinha/agentic-orchestration-framework):
two processes that talk over IDL interfaces, in C, C++, Python, Perl and MATLAB.

| Repo | Process | Role |
|---|---|---|
| [pw-server](https://github.com/meenusinha/pw-server) | `authd` | defines and serves `Auth::IPasswordService` (IDL); calls back `SessionEvents::ISessionListener` |
| [pw-client](https://github.com/meenusinha/pw-client) | `ui-shell` | calls `IPasswordService` from C++, C and Python; defines and implements `ISessionListener` (in-house `.xidl`) |

### Try it

1. Clone both repos anywhere, or let the framework's setup GUI clone them for you
   (repository URL + branch `main`).
2. Run the framework's setup GUI (`python3 setup_gui.py` in the framework clone) and add
   both repos in step 3.
3. In step 4 (Review) the GUI asks what the unknown file types contain:
   `.xcfg` (pw-server) is server configuration, `.xidl` (pw-client) is an in-house IDL dialect.
4. Create the GraphRAG and ask, for example:
   - Search: `which processes are affected if PWD_MIN_LEN changes?`
   - Trace interface: `IPasswordService`
   - Impact of change: `pwd_policy_check`

### Branches

- `main` — the baseline.
- `policy-hint` (pw-client only) — the login dialog shows the password policy when it
  opens, reading the new caller of the IDL attribute `minLength`. Clone pw-client with
  this branch (or switch an existing clone to it) to see the graph pick up a change.

`src/db_config.cpp` in pw-server contains **fake** credentials on purpose, to show that
secrets are redacted before indexing.
