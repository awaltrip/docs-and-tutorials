# Resolving npm audit issues

1. Run `npm i` on your local to make sure everything is up to date.
2. Run `npm audit` on your local.
3. If CVEs exist, run `npm audit fix` to introduce non-breaking upgrades.
    - **Do NOT run** `npm audit fix --force` as this could introduce breaking changes into the codebase.
    - **NOTE:** If the repo does not allow commits of a lock file, step 3 may not be helpful.
4. If CVEs still exist, see if there are any you can manually upgrade which are non-breaking (it should state this in the `npm audit` results).
5. At this point, run your local CI-checks, then commit any changes you can to Git.
    - the app might include an `npm run ci-check` script in its `package.json`

If CVEs still exist:

6. Run `npm install -g npm-audit-resolver` (if you've never installed it before).
7. If the app uses a shared audit file, run `copy .\file-path\audit-resolve.json .`
    - for Unix terminals, run `cp ./file-path/audit-resolve.json .`
8. Run `resolve-audit`
    - For each vulnerability type `i` to ignore path, then `M` to do so for 1 month.
    - This will add an entry automatically to `audit-resolve.json` for each vulnerability.
9. Run `check-audit`. At this point, it will return "audit ok" if each vulnerability has been fixed or added to the `audit-resolve.json`. If it does not return "audit ok", try the previous step again.
10. If the app uses a shared audit file, clone that repo to your local. Copy your updates to `audit-resolve.json` into the file in that repo, and open a PR against the relevant branch.
