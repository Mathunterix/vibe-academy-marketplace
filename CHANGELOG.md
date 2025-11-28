# changelog

toutes les modifications notables de ce projet seront documentées ici.

le format est basé sur [keep a changelog](https://keepachangelog.com/en/1.0.0/),
et ce projet adhère au [semantic versioning](https://semver.org/spec/v2.0.0.html).

## [unreleased]

### prochainement
- agents supplémentaires pour exploration avancée
- commands pour workflows spécifiques
- skills additionnels selon besoins utilisateurs

## [1.0.0] - 2025-11-28

### added

**agents:**
- agent deep-search (1-vibeplanning) - recherche approfondie avec brightdata/brave/websearch
- agent explore-codebase (1-vibeplanning) - exploration spécialisée de codebase

**commands:**
- command create-plan (2-context-engineering) - créer plan d'implémentation à partir requirements
- command execute-plan (3-implementation) - exécuter plan avec task management archon (optionnel)
- command prompt-agent (6-extra) - créer et optimiser prompts d'agents
- command prompt-command (6-extra) - créer et optimiser prompts de commands
- command start-session (8-documentation) - initialiser session avec memory bank context
- command update-docs-command (8-documentation) - mettre à jour docs avec auto-archiving

**skills:**
- skill archon - intégration archon via rest api (knowledge base, projects, tasks, documents, versioning)

**infrastructure:**
- marketplace.json configuré pour distribution
- plugin.json avec métadonnées complètes
- organisation en sous-dossiers pour agents et commands
- README.md dual-platform (claude code + claude desktop)
- documentation complète dans docs/
- guide marketplace hybride complet

**features:**
- support claude code via marketplace natif
- support claude desktop via .zip releases
- graceful degradation (fonctionne avec ou sans dépendances)
- archon optionnel (rest api via skill)
- brightdata/brave search optionnels (fallback sur websearch)

### changed
- aucun changement (première release)

### deprecated
- aucune dépréciation

### removed
- aucune suppression

### fixed
- aucun fix (première release)

### security
- aucun problème de sécurité

---

[unreleased]: https://github.com/vibeacademy/vibe-academy-marketplace/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/vibeacademy/vibe-academy-marketplace/releases/tag/v1.0.0
