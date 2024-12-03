# liste_etudiants_php
<?php
try {
    $db = new PDO('mysql:host=localhost;dbname=upb_bd_td_techno_web;charset=utf8', 'root', '');
} catch (Exception $e) {
    die('Erreur : ' . $e->getMessage());
}

// Récupérer tous les étudiants
$sqlQuery = 'SELECT * FROM etudiants';
$etudiantsStatement = $db->prepare($sqlQuery);
$etudiantsStatement->execute();
$etudiants = $etudiantsStatement->fetchAll();
?>

<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Liste des Étudiants</title>
</head>
<body>
    <h1>Liste des Étudiants</h1>
    <a href="ajout_etudiant.php">Ajouter un Étudiant</a>
    <table border="1">
        <tr>
            <th>ID</th>
            <th>Nom</th>
            <th>Prénoms</th>
            <th>Genre</th>
            <th>Email</th>
            <th>Quartier</th>
            <th>Contact</th>
            <th>Actions</th>
        </tr>
        <?php foreach ($etudiants as $etudiant): ?>
        <tr>
            <td><?php echo $etudiant['id']; ?></td>
            <td><?php echo $etudiant['nom']; ?></td>
            <td><?php echo $etudiant['prenoms']; ?></td>
            <td><?php echo $etudiant['genre']; ?></td>
            <td><?php echo $etudiant['email']; ?></td>
            <td><?php echo $etudiant['quartier']; ?></td>
            <td><?php echo $etudiant['contact']; ?></td>
            <td>
                <th><a href="details_etudiant.php?id_etudiant=<?php echo $etudiant['id']; ?>">Voir plus</a></th>
                <th><a href="modifier_etudiant.php?id_etudiant=<?php echo $etudiant['id']; ?>">Modifier</a></th>
                <th><a href="supprimer_etudiant.php?id_etudiant=<?php echo $etudiant['id']; ?>">Supprimer</a></th>
            </td>
        </tr>
        <?php endforeach; ?>
    </table>
</body>
</html>
