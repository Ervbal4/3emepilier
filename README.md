# 3emepilier<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Économisez avec le 3e Pilier - Calculateur</title>
<style>
  body {
    font-family: 'Arial', sans-serif;
    background: #f7f9fc;
    margin: 0; padding: 0;
    color: #333;
  }
  header {
    background-color: #005a9c;
    color: white;
    padding: 2rem 1rem;
    text-align: center;
  }
  header h1 {
    margin: 0;
    font-size: 2rem;
  }
  header p {
    font-size: 1.2rem;
    margin-top: 0.5rem;
  }
  main {
    max-width: 600px;
    background: white;
    margin: -40px auto 2rem auto;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 8px 20px rgb(0 0 0 / 0.1);
  }
  form label {
    display: block;
    margin-top: 1rem;
    font-weight: bold;
  }
  form select,
  form input[type="number"],
  form input[type="text"],
  form input[type="email"],
  form input[type="tel"] {
    width: 100%;
    padding: 0.6rem;
    margin-top: 0.3rem;
    border-radius: 4px;
    border: 1px solid #ccc;
    font-size: 1rem;
  }
  form button {
    margin-top: 1.8rem;
    width: 100%;
    padding: 1rem;
    background-color: #005a9c;
    color: white;
    font-size: 1.2rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  form button:hover {
    background-color: #004080;
  }
  .result {
    margin-top: 1.5rem;
    padding: 1rem;
    background-color: #d7f0d8;
    border: 1px solid #2e8b57;
    border-radius: 6px;
    font-weight: bold;
    font-size: 1.1rem;
    text-align: center;
    display: none;
  }
  footer {
    text-align: center;
    font-size: 0.9rem;
    color: #777;
    padding: 2rem 1rem;
  }
</style>
</head>
<body>

<header>
  <h1>Économisez jusqu’à CHF 2'900 d’impôt avec le 3e Pilier</h1>
  <p>Calculez en 1 minute combien vous pouvez économiser grâce au pilier 3a</p>
</header>

<main>
  <form id="taxForm">
    <label for="canton">Dans quel canton vivez-vous ?</label>
    <select id="canton" required>
      <option value="">Sélectionnez un canton</option>
      <option value="genève">Genève</option>
      <option value="vaud">Vaud</option>
      <option value="valais">Valais</option>
      <option value="zurich">Zurich</option>
      <option value="neuchatel">Neuchâtel</option>
      <option value="autre">Autre</option>
    </select>

    <label for="revenu">Votre revenu annuel brut (CHF)</label>
    <input type="number" id="revenu" placeholder="Ex. 80000" min="0" required />

    <label>Statut marital</label>
    <select id="statut" required>
      <option value="">Sélectionnez votre statut</option>
      <option value="celibataire">Célibataire</option>
      <option value="marie">Marié(e)</option>
    </select>

    <label>Avez-vous des enfants à charge ?</label>
    <select id="enfants" required>
      <option value="">Sélectionnez</option>
      <option value="oui">Oui</option>
      <option value="non">Non</option>
    </select>

    <label for="montant">Montant que vous comptez verser dans un pilier 3a (CHF)</label>
    <input type="number" id="montant" placeholder="Ex. 6883" min="0" max="36288" required />

    <button type="submit">Calculer mon économie d’impôt</button>

    <div class="result" id="result"></div>
  </form>
</main>

<footer>
  &copy; 2025 Votre Cabinet d’Assurance - Tous droits réservés
</footer>

<script>
  // Taux d'imposition marginal estimés par canton (exemples)
  const tauxImposition = {
    geneve: 0.25,
    vaud: 0.22,
    valais: 0.20,
    zurich: 0.23,
    neuchatel: 0.21,
    autre: 0.20
  };

  document.getElementById('taxForm').addEventListener('submit', function(e) {
    e.preventDefault();

    const canton = document.getElementById('canton').value;
    const revenu = parseFloat(document.getElementById('revenu').value);
    const statut = document.getElementById('statut').value;
    const enfants = document.getElementById('enfants').value;
    const montant = parseFloat(document.getElementById('montant').value);

    if (!canton || isNaN(revenu) || !statut || !enfants || isNaN(montant)) {
      alert('Merci de remplir tous les champs correctement.');
      return;
    }

    // Taux d'imposition de base selon canton
    let taux = tauxImposition[canton] || 0.20;

    // Ajustement simplifié du taux selon statut marital et enfants
    if (statut === 'marie') taux -= 0.03;
    if (enfants === 'oui') taux -= 0.02;

    // Calcul économie fiscale estimée
    // Limite max 3e pilier: 7'258 CHF pour salariés, 36'288 pour indépendants
    // Ici on simplifie en plafonnant à 7'258
    const plafond = 7258;
    const baseCalcul = Math.min(montant, plafond);
    const economie = Math.round(baseCalcul * taux);

    // Affichage résultat
    const resultDiv = document.getElementById('result');
    resultDiv.style.display = 'block';
    resultDiv.textContent = `🎉 Vous pouvez économiser environ CHF ${economie} d’impôt cette année grâce au 3e pilier !`;

  });
</script>

</body>
</html>
