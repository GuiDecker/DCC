# Agent Orkestrasyonu

## Mevcut Agent'lar

ECC agent'ları `ecc@ecc` eklentisiyle birlikte gelir, `~/.claude/agents/` dizininde bulunmaz.
Agent aracıyla eklenti kapsamlı bir `subagent_type` ile çağrılır:

```text
Agent(subagent_type: "dcc:planner", prompt: "...")
```

| Agent | Amaç | Ne Zaman Kullanılır |
|-------|---------|-------------|
| dcc:planner | Uygulama planlaması | Karmaşık özellikler, refactoring |
| dcc:architect | Sistem tasarımı | Mimari kararlar |
| dcc:tdd-guide | Test odaklı geliştirme | Yeni özellikler, hata düzeltmeleri |
| dcc:code-reviewer | Kod incelemesi | Kod yazdıktan sonra |
| dcc:security-reviewer | Güvenlik analizi | Commit'lerden önce |
| dcc:build-error-resolver | Build hatalarını düzeltme | Build başarısız olduğunda |
| dcc:e2e-runner | E2E testleri | Kritik kullanıcı akışları |
| dcc:refactor-cleaner | Ölü kod temizliği | Kod bakımı |
| dcc:doc-updater | Dokümantasyon | Dokümanları güncelleme |
| dcc:rust-reviewer | Rust kod incelemesi | Rust projeleri |

68 agent'ın tam listesi için `/ecc:ecc-guide` bölümüne bakın.

## Anlık Agent Kullanımı

Kullanıcı istemi gerekmez:
1. Karmaşık özellik istekleri - **dcc:planner** agent kullan
2. Kod yeni yazıldı/değiştirildi - **dcc:code-reviewer** agent kullan
3. Hata düzeltmesi veya yeni özellik - **dcc:tdd-guide** agent kullan
4. Mimari karar - **dcc:architect** agent kullan

## Paralel Görev Yürütme

Bağımsız işlemler için DAIMA paralel Task yürütme kullan:

```markdown
# İYİ: Paralel yürütme
3 agent'ı paralel başlat:
1. Agent 1: Auth modülü güvenlik analizi
2. Agent 2: Cache sistemi performans incelemesi
3. Agent 3: Utilities tip kontrolü

# KÖTÜ: Gereksiz sıralı yürütme
Önce agent 1, sonra agent 2, sonra agent 3
```

## Çok Perspektifli Analiz

Karmaşık problemler için split role sub-agent'lar kullan:
- Factual reviewer
- Senior engineer
- Security expert
- Consistency reviewer
- Redundancy checker
