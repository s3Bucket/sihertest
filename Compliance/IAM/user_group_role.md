### Übungsaufgabe 1: IAM Benutzer erstellen und konfigurieren
1. **Aufgabe**: Erstelle einen neuen IAM Benutzer `Siher`.
2. **Schritte**:
    - Navigiere zur AWS Konsole.
    - Gehe zum Service "IAM" und dann links auf "Benutzer"
    - Klicke auf "Benutzer hinzufügen".
    - Gib `Siher` als Benutzernamen ein.
    - Weise dem Benutzer eine Berechtigung zu.
   
   **Zusatzaufgabe**:
    - Erstelle ein Schlüsselpaar (Access Key ID und Secret Access Key) und speichere diese sicher.
3. **Fragen**:
   - Wie kannst du sicherstellen, dass der Benutzer `Siher` nur bestimmte Aktionen in AWS ausführen kann?
   - Was sind 'Policies'? Wofür werden diese gebraucht?
   - Ein Benutzer hat weder die Berechtigung, noch ein Verbot um EC2-Instanzen zu administrieren. Kann er das dann machen?

### Übungsaufgabe 2: IAM Gruppe erstellen und Berechtigungen zuweisen
1. **Aufgabe**: Erstelle eine neue IAM Gruppe namens `Praktikanten`.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Klicke auf "Gruppen" und dann auf "Neue Gruppe erstellen".
    - Gib `Praktikanten` als Gruppennamen ein.
    - Weisen der Gruppe eine Richtlinie zu.
3. **Frage**: 
   - Welche Berechtigungen hat ein Benutzer, der Mitglied der Gruppe `Praktikanten` ist?
   - Ein Benutzer hat die Berechtigung "AmazonEC2FullAccess" mit der er EC2-Instanzen administrieren kann. Gleichzeitig
   gleichzeititg ister aber auch in einer Gruppe, die den Zugriff auf "AmazonEC2FullAccess" verbietet. Kann der Benutzer 
   EC2-Instanzen administrieren?

### Übungsaufgabe 3: Benutzer einer Gruppe hinzufügen
1. **Aufgabe**: Füge den Benutzer `Siher` zur Gruppe `Praktikanten` hinzu.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Wähle "Benutzer" aus und klicke auf `Siher`.
    - Klicke auf die Registerkarte "Gruppen" und füge `Siher` zur Gruppe `Praktikanten` hinzu.
3. **Frage**: Welche zusätzlichen Berechtigungen erhält der Benutzer `Siher` durch die Mitgliedschaft in der Gruppe `Praktikanten`?

### Übungsaufgabe 4: IAM Rolle erstellen und verwenden
1. **Aufgabe**: Erstelle eine neue IAM Rolle namens `LambdaExecutionRole`.
2. **Schritte**:
    - Navigiere zur IAM Konsole.
    - Klicke auf "Rollen" und dann auf "Rolle erstellen".
    - Wähle den Anwendungsfall "Lambda" aus.
    - Weisen der Rolle die `AWSLambdaBasicExecutionRole` Richtlinie zu.
3. **Frage**: Welche Art von Zugriff wird der `LambdaExecutionRole` gewährt?

### Zusatzaufgabe: Rolle an eine Lambda-Funktion anhängen
1. **Aufgabe**: Erstelle eine neue Lambda-Funktion und weise ihr die Rolle `LambdaExecutionRole` zu.
2. **Schritte**:
    - Navigiere zur Lambda Konsole.
    - Klicke auf "Funktion erstellen".
    - Gib der Funktion einen Namen (z.B. `TestLambdaFunction`).
    - Wähle als Ausführungsrolle die existierende Rolle `LambdaExecutionRole` aus.
3. **Frage**: Warum ist es wichtig, dass Lambda-Funktionen die richtigen Rollen zugewiesen bekommen?
