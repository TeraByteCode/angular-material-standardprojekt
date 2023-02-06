# Angular Material Standardprojekt

Dieses Projekt dient als Vorlagenprojekt, um Angurlar-Projekte mit Material Design zu realisieren.

Alle AddOns und Funktionen, habe ich mit Kommentare versehen, um zu wissen warum oder wofür sie gut sind.

**Die folgenden Dateien wurden bearbeitet oder ergänzt:**

- .vscode\extensions.json
- .vscode\settings.json

**Die folgenden Dev. Tools wurden hinzugefügt:**

- Conventionalcommits
- Commitlint
- GitHooks

### Warum konventionelle Commits verwenden?

- Ermöglicht die automatische Erstellung der CHANGELOG-Datei.
- Automatische Ermittlung von Versionsänderungen nach SemVer (basierend auf den verwendeten Commit-Typen).
- Teit den anderen Teammitgliedern oder anderen interessierten Personen die Art der Änderungen mit.
- Auslösen der Build- und Deployment- oder Release-Prozesse.
- Erleichtert anderen, zum Projekt beizutragen, indem man erlaubt, die Commit-Historie auf strukturiertere Weise zu erkunden.

# VSCode Arbeitsumgebung Vorbereiten

## Commitlint, Conventionalcommits und Husky

```sh
npm i --save-dev @commitlint/cli @commitlint/config-conventional
```

Erstelle die Datei commitlint-config.js in das Stammverzeichnis ein, damit erbt commitlint die Normen von Conventionalcommits

```sh
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

Hier werden wir Husky verwende um die Commits zu verbessern.
Es kann aber auch zum Ausführen von Tests, zum Linting von Code usw. sowie vor oder nach einem Commit oder push verwendet werden.
[Wenn es zu dem Fehler kommt, findest du hier Hilfe](https://stackoverflow.com/questions/63244379/how-to-fix-syntaxerror-invalid-or-unexpected-token-when-trying-to-run-node-js)

```sh
npm i -D husky
```

Damit fügen wir husky install zur package.json hinzu

```sh
npm pkg set scripts.prepare="husky install"
```

Husky im Projekt installieren:

```sh
npm run prepare
```

Wir fügen nun eine neue Regel zum Pre-Commit-Hook hinzu, um zu prüfen und zu validieren, ob die Commit-Nachricht den Regeln der Conventional-Commits-Konvention entspricht. Das muss nur einmal ausgeführt werden.

```sh
npx husky add .husky/commit-msg "npx --no -- commitlint --edit ${1}"
```

Wenn man jetzt eine unkonventionelle Commit erstellt, erhält man eine Meldung:

```sh
git add .
git commit -am 'test'

⧗   input: test
✖   Please add rules to your `commitlint.config.js`
    - Getting started guide: https://commitlint.js.org/#/?id=getting-started
    - Example config: https://github.com/conventional-changelog/commitlint/blob/master/%40commitlint/config-conventional/index.js [empty-rules]

✖   found 1 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

husky - commit-msg hook exited with code 1 (error)
```

Conventional-Changelog installieren:

```sh
npm i -g conventional-changelog-cli
```

CHANGELOG Alias einrichten:

```sh
npm pkg set scripts.changelog="conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
```

mit `npm run changelog` wird der Alias ausgeführt

Nützliche Links:

- https://commitlint.js.org/
