# LAZTAR-trainee-notes

Daily learning journal, technical notes and lessons learned during my trainee journey at Công ty trách nhiệm hữu hạn LAZTAR - Phần Mềm & Giải Pháp Số (Software & Digital).

## Hugo site

This repository is set up as a Hugo documentation site using `hugo-theme-learn`.

Local preview:

```bash
hugo server
```

Build:

```bash
hugo --minify
```

## Content format

Use the same bilingual file pattern for new weeks and days:

```text
content/
  week-02/
    _index.md
    _index.vi.md
    day-02.md
    day-02.vi.md
    day-03.md
    day-03.vi.md
```

English pages use `.md`; Vietnamese pages use `.vi.md`. Keep the same slug in both files so the language switcher can map routes correctly, for example:

```text
/week-02/day-02/
/vi/week-02/day-02/
```

Suggested commands:

```bash
hugo new --kind week week-02/_index.md
hugo new --kind week week-02/_index.vi.md
hugo new --kind day week-02/day-02.md
hugo new --kind day week-02/day-02.vi.md
```

GitHub Pages URL after deployment:

```text
sharonng1029.github.io/LAZTAR-PEEP2026-Trainee-Notes/
```

Deployment is handled by `.github/workflows/hugo.yml`. In GitHub, enable:

Settings -> Pages -> Build and deployment -> Source -> GitHub Actions
