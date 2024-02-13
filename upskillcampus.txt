import os
import shutil

def organize_files(directory):
    extensions_folders = {
        "Images": [".jpeg", ".jpg", ".png", ".gif", ".bmp"],
        "Documents": [".doc", ".docx", ".pdf", ".txt", ".xlsx", ".pptx"],
        "Videos": [".mp4", ".mkv", ".avi", ".mov", ".flv"],
        "Music": [".mp3", ".wav", ".flac", ".aac"],
        "Archives": [".zip", ".rar", ".tar", ".gz"],
        "Programs": [".exe", ".msi"]
        # Add more categories as needed
    }

    for folder in extensions_folders:
        folder_path = os.path.join(directory, folder)
        if not os.path.exists(folder_path):
            os.makedirs(folder_path)

    for filename in os.listdir(directory):
        if os.path.isfile(os.path.join(directory, filename)):
            file_ext = os.path.splitext(filename)[1].lower()
            dest_folder = "Others"
            for folder, ext_list in extensions_folders.items():
                if file_ext in ext_list:
                    dest_folder = folder
                    break
            src_path = os.path.join(directory, filename)
            dest_path = os.path.join(directory, dest_folder, filename)
            shutil.move(src_path, dest_path)
            print(f"Moved {filename} to {dest_folder} folder.")

if __name__ == "__main__":
    directory_to_organize = input("Enter the directory path to organize: ")
    organize_files(directory_to_organize)
    print("Files have been organized successfully!")
