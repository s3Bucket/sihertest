### Übungsaufgabe 1: Erstellen einer benutzerdefinierten Richtlinie
1. **Aufgabe**: Erstelle eine benutzerdefinierte IAM-Richtlinie namens `S3FullAccessPolicy`, die einem Benutzer vollen Zugriff auf Amazon S3 gewährt.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Klicke auf "Richtlinien" und dann auf "Richtlinie erstellen".
    - Wähle den JSON-Editor und füge die folgende Richtlinie ein:
      ```json
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
          }
        ]
      }
      ```
    - Überprüfe die Richtlinie und gib ihr den Namen `S3FullAccessPolicy`.
3. **Frage**: Welche Risiken sind mit einer so weitreichenden Richtlinie verbunden?

### Übungsaufgabe 2: Anfügen einer Richtlinie an einen Benutzer
1. **Aufgabe**: Füge die `S3FullAccessPolicy` Richtlinie dem Benutzer `Siher` hinzu.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Wähle "Benutzer" aus und klicke auf `Siher`.
    - Klicke auf die Registerkarte "Anfügen von Richtlinien".
    - Suche nach `S3FullAccessPolicy` und füge sie hinzu.
3. **Frage**: Welche Aktionen kann `Siher` nun in Amazon S3 ausführen?

### Übungsaufgabe 3: Erstellen einer Richtlinie mit eingeschränktem Zugriff
1. **Aufgabe**: Erstelle eine benutzerdefinierte Richtlinie namens `ReadOnlyEC2Policy`, die einem Benutzer nur Lesezugriff auf Amazon EC2 gewährt.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Klicke auf "Richtlinien" und dann auf "Richtlinie erstellen".
    - Wähle den JSON-Editor und füge die folgende Richtlinie ein:
      ```json
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "ec2:Describe*"
            ],
            "Resource": "*"
          }
        ]
      }
      ```
    - Überprüfe die Richtlinie und gib ihr den Namen `ReadOnlyEC2Policy`.
3. **Fragen**: 
   - Warum ist es manchmal besser, eine Richtlinie mit eingeschränktem Zugriff zu erstellen?
   - Was ist mit "least privileges" gemeint?

### Übungsaufgabe 4: Anfügen einer Richtlinie an eine Gruppe
1. **Aufgabe**: Füge die `ReadOnlyEC2Policy` Richtlinie der Gruppe `Praktikanten` hinzu.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Wähle "Gruppen" aus und klicke auf `Praktikanten`.
    - Klicke auf die Registerkarte "Anfügen von Richtlinien".
    - Suche nach `ReadOnlyEC2Policy` und füge sie hinzu.
3. **Frage**: Welche Auswirkungen hat dies auf alle Mitglieder der Gruppe `Entwickler`?

### Übungsaufgabe 5: Überprüfen von Richtlinien und Berechtigungen
1. **Aufgabe**: Überprüfe die effektiven Berechtigungen eines Benutzers in AWS IAM.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Wähle "Benutzer" aus und klicke auf `Praktikant1`.
    - Klicke auf die Registerkarte "Berechtigungsübersicht".
    - Überprüfe die angezeigten Richtlinien und effektiven Berechtigungen.
3. **Frage**: Wie kannst du sicherstellen, dass ein Benutzer nicht mehr Berechtigungen hat, als er benötigt?

Hier sind zwei zusätzliche Übungsaufgaben zum Thema implizites und explizites Verweigern (implicit and explicit deny) in AWS IAM:

### Übungsaufgabe 6: Explizites Verweigern einführen
1. **Aufgabe**: Erstelle eine benutzerdefinierte Richtlinie namens `DenyS3DeletePolicy`, die das Löschen von Objekten in allen S3-Buckets explizit verweigert.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Klicke auf "Richtlinien" und dann auf "Richtlinie erstellen".
    - Wähle den JSON-Editor und füge die folgende Richtlinie ein:
      ```json
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Deny",
            "Action": "s3:DeleteObject",
            "Resource": "arn:aws:s3:::*/*"
          }
        ]
      }
      ```
    - Überprüfe die Richtlinie und gib ihr den Namen `DenyS3DeletePolicy`.
3. **Frage**: Was passiert, wenn ein Benutzer mit dieser Richtlinie versucht, ein Objekt in S3 zu löschen?

### Übungsaufgabe 7: Testen von implizitem und explizitem Verweigern
1. **Aufgabe**: Teste die Auswirkungen von explizitem und implizitem Verweigern auf einen Benutzer.
2. **Schritte**:
    - Erstelle einen Benutzer `Colin`.
    - Weisen dem Benutzer die `S3FullAccessPolicy` und die `DenyS3DeletePolicy` Richtlinien zu.
    - Versuche, als Benutzer `Colin` ein Objekt in einem S3-Bucket zu erstellen und zu löschen.
3. **Frage**: Welche Aktionen kann `Colin` in S3 ausführen und warum? Erkläre den Unterschied zwischen implizitem und explizitem Verweigern.

### Erklärung der Konzepte:
- **Implizites Verweigern (Implicit Deny)**: Alle Aktionen, die nicht explizit durch eine Richtlinie erlaubt sind, werden standardmäßig verweigert. Wenn keine Richtlinie eine bestimmte Aktion erlaubt, wird diese Aktion verweigert, auch ohne eine explizite "Deny"-Regel.
- **Explizites Verweigern (Explicit Deny)**: Eine explizite "Deny"-Regel in einer Richtlinie hat Vorrang vor allen "Allow"-Regeln. Selbst wenn eine andere Richtlinie eine Aktion erlaubt, wird die Aktion verweigert, wenn eine "Deny"-Regel sie explizit verbietet.
