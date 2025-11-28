# vibe academy marketplace

agents, commands et skills pour maîtriser le développement avec claude code.

[![version](https://img.shields.io/github/v/release/vibeacademy/vibe-academy-marketplace)](https://github.com/vibeacademy/vibe-academy-marketplace/releases)
[![license](https://img.shields.io/github/license/vibeacademy/vibe-academy-marketplace)](LICENSE)

## 🚀 installation rapide

### pour claude code (recommandé)

```bash
# ajouter le marketplace
/plugin marketplace add vibeacademy/vibe-academy-marketplace

# installer le plugin
/plugin install vibe-academy@vibe-academy-marketplace

# vérifier l'installation
/help
```

### pour claude desktop

1. aller sur [releases](https://github.com/vibeacademy/vibe-academy-marketplace/releases/latest)
2. télécharger le skill .zip souhaité (ex: `archon-v1.0.0.zip`)
3. ouvrir claude desktop → settings → capabilities → skills
4. cliquer "upload skill"
5. sélectionner le .zip téléchargé
6. toggle on pour activer

## 📚 contenu

### agents (2)

**deep-search** (1-vibeplanning)
- recherche approfondie sur un sujet précis
- utilise brightdata (prioritaire), brave search, websearch
- génère analyse détaillée dans /docs/deepsearch/
- parfait pour: recherche documentaire, comparaison technologies, best practices

**explore-codebase** (1-vibeplanning)
- exploration spécialisée de codebase
- trouve patterns, dépendances, points d'intégration
- stratégie: grep → parallel searches → follow imports
- parfait pour: comprendre architecture, trouver similar features

### commands (6)

**create-plan** (2-context-engineering)
```bash
/create-plan path/to/requirements.md
```
- crée plan d'implémentation complet à partir de requirements
- recherche best practices, patterns existants
- génère document plan exécutable dans PRPs/
- intégration archon optionnelle (si mcp installé)

**execute-plan** (3-implementation)
```bash
/execute-plan path/to/plan.md
```
- exécute plan de développement avec task management
- cycle: todo → doing → review → done
- validation automatique avec validator agent
- intégration archon optionnelle

**prompt-agent** (6-extra)
```bash
/prompt-agent create my-agent
/prompt-agent refactor @agents/existing.md
```
- crée et optimise prompts d'agents
- templates pour: search/exploration, modification, analysis
- patterns et best practices intégrés

**prompt-command** (6-extra)
```bash
/prompt-command create my-command
/prompt-command refactor @commands/existing.md
```
- crée et optimise prompts de commands
- patterns: numbered workflow, reference/docs, analysis
- génère structure optimale automatiquement

**start-session** (8-documentation)
```bash
/start-session
```
- initialise session de travail avec contexte documentation
- affiche memory bank: product, tech, patterns, active work
- parfait pour: reprendre projet, onboarding équipe

**update-docs-command** (8-documentation)
```bash
/update-docs-command
```
- met à jour memory bank après session
- auto-archive entrées anciennes (garde seulement récent)
- structure: progress, active-context, decision-log
- token-efficient, pas de questions redondantes

### skills (1)

**archon**
- intégration archon pour knowledge base et project management
- utilise rest api (pas besoin du mcp si pas installé)
- fonctionnalités:
  - rag-powered semantic search
  - gestion projets/tasks hiérarchique
  - website crawling et document upload
  - versioning de documents
- endpoints: knowledge, projects, tasks, documents, versions

## 🔄 mise à jour

### claude code
```bash
/plugin update vibe-academy
```

### claude desktop
télécharger nouvelle version depuis [releases](https://github.com/vibeacademy/vibe-academy-marketplace/releases) et re-upload.

## 🎯 cas d'usage

### recherche et exploration

**recherche documentaire approfondie:**
```bash
# lancer deep-search agent via task tool
"fais une recherche approfondie sur les meilleures pratiques de testing react"
```

**explorer codebase pour feature:**
```bash
# lancer explore-codebase agent
"explore le codebase pour comprendre comment l'authentification fonctionne"
```

### planning et implémentation

**créer plan d'implémentation:**
```bash
# créer requirements.md puis:
/create-plan requirements/new-feature.md
# génère PRPs/new-feature.md avec plan complet
```

**exécuter plan avec task tracking:**
```bash
/execute-plan PRPs/new-feature.md
# implémente avec task management archon (optionnel)
```

### documentation et workflow

**démarrer session de travail:**
```bash
/start-session
# affiche contexte actuel: features in progress, tech stack, patterns
```

**mettre à jour docs après session:**
```bash
/update-docs-command
# update progress.md, active-context.md, decision-log.md
# auto-archive si trop d'entrées
```

### méta - créer ses propres outils

**créer nouvel agent:**
```bash
/prompt-agent create my-specialized-agent
# génère structure avec best practices
```

**créer nouvelle command:**
```bash
/prompt-command create my-workflow
# génère template optimisé
```

## 📦 dépendances optionnelles

### archon skill

**si vous voulez archon:**
- installer archon server via docker
- configurer url (default: http://localhost:8181)
- le skill gère le reste via rest api

**si vous ne voulez pas archon:**
- commands create-plan et execute-plan fonctionnent sans (skip archon steps)
- skill archon simplement ignoré

### deep-search agent

**mcp recommandés** (graceful degradation):
- brightdata (prioritaire) - scraping et recherche avancée
- brave-search (fallback) - recherche rapide
- websearch/webfetch (dernier recours) - built-in

l'agent s'adapte automatiquement aux outils disponibles.

### aucune dépendance obligatoire

tout fonctionne out-of-the-box avec outils built-in de claude code.

## 🏗️ organisation

### structure avec sous-dossiers

les agents et commands sont organisés par catégories:

**agents:**
- `1-vibeplanning/` - recherche et exploration

**commands:**
- `2-context-engineering/` - planning
- `3-implementation/` - exécution
- `6-extra/` - méta-outils (créer agents/commands)
- `8-documentation/` - workflow documentation

**skills:**
- structure plate standard

cette organisation facilite la navigation et la compréhension du workflow complet.

## 🤝 contribution

voir [CONTRIBUTING.md](docs/CONTRIBUTING.md)

## 📄 license

MIT - voir [LICENSE](LICENSE)

## 🔗 liens

- [documentation complète](docs/GETTING-STARTED.md)
- [guide marketplace hybride](../docs/GUIDE-MARKETPLACE-HYBRIDE.md)
- [issues](https://github.com/vibeacademy/vibe-academy-marketplace/issues)
- [vibe academy](https://vibeacademy.com)

---

**note**: ce marketplace est conçu pour fonctionner avec ou sans dépendances externes. les intégrations archon et brightdata sont optionnelles et améliorent l'expérience mais ne sont pas requises.
