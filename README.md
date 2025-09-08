import os
import shutil

# File type mapping
FILE_TYPES = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Documents": [".pdf", ".docx", ".txt", ".pptx"],
    "Videos": [".mp4", ".mkv", ".mov"],
    "Audio": [".mp3", ".wav"],
    "Archives": [".zip", ".rar", ".tar"]
}

def organize_files(folder_path):
    for filename in os.listdir(folder_path):
        file_path = os.path.join(folder_path, filename)

        if os.path.isfile(file_path):
            moved = False
            for folder, extensions in FILE_TYPES.items():
                if filename.lower().endswith(tuple(extensions)):
                    folder_name = os.path.join(folder_path, folder)
                    os.makedirs(folder_name, exist_ok=True)
                    shutil.move(file_path, os.path.join(folder_name, filename))
                    moved = True
                    break

            if not moved:  # Others folder
                other_folder = os.path.join(folder_path, "Others")
                os.makedirs(other_folder, exist_ok=True)
                shutil.move(file_path, os.path.join(other_folder, filename))

if __name__ == "__main__":
    path = input("Enter folder path: ")
    organize_files(path)
    print("✅ Files Organized Successfully!")
