---
comments: ture
---

# Material Mkdocs - Buttons

## 설정

```yaml title="mkdocs.yml"
markdown_extensions:
  - attr_list
```

## 사용법

### Button 추가

```yaml title="Button"
[Subscribe to our newsletter](#){ .md-button }
```

[Subscribe to our newsletter](#){ .md-button }

### 색이 있는 Button 추가

```yaml title="Button"
[Subscribe to our newsletter](#){ .md-button .md-button--primary }
```

[Subscribe to our newsletter](#){ .md-button .md-button--primary }

### Icon이 있는 Button 추가

```yaml title="Button"
[Send :fontawesome-solid-paper-plane:](#){ .md-button }
```

[Send :fontawesome-solid-paper-plane:](#){ .md-button }
