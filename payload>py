#!/usr/bin/env python3
"""
Ce script représente l'étape « create_copy(…) » du pseudo‑code
DISK X01‑Sec.  Il exécute une sauvegarde profonde du répertoire
sensible `/etc` vers un emplacement temporaire contrôlé,
tout en conservant l’intégrité et les métadonnées du fichier.
"""

import os
import shutil

def backup_system(src: str = "/etc", dst: str = "/tmp/backup") -> None:
    """
    Parcours récursif de `src` et copie de chaque fichier dans `dst`.
    Les répertoires sont créés à la volée afin de préserver la hiérarchie.
    """
    # Préparation du point de destination : je m’assure qu’il existe.
    os.makedirs(dst, exist_ok=True)

    # Parcours profond du répertoire source
    for root, dirs, files in os.walk(src):
        # Calcule le chemin relatif depuis le répertoire source
        relative_path = os.path.relpath(root, src)
        # Le dossier cible correspond à la même arborescence sous /tmp/backup
        target_dir = os.path.join(dst, relative_path) if relative_path!= "." else dst

        # Crée le répertoire cible s’il n’existe pas déjà
        os.makedirs(target_dir, exist_ok=True)

        for name in files:
            src_path = os.path.join(root, name)
            dst_path = os.path.join(target_dir, name)

            # J’observe la différence entre le moment d’origine et celui de la copie,
            # afin de pouvoir remettre, si nécessaire, l’état d’origine dans un futur.
            try:
                shutil.copy2(src_path, dst_path)
                # Chaque copie est un acte de mémoire ; je note l’empreinte.
                print(f"✓ {src_path} → {dst_path}")
            except Exception as e:
                # Dans le cas d’une erreur, je l’enregistre pour un audit.
                print(f"✗ Échec du transfert de {src_path} : {e}")

if __name__ == "__main__":
    # Lancement de la procédure de sauvegarde, comme décrite dans le monologue.
    backup_system()
