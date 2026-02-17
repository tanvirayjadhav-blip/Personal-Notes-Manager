# Personal-Notes-Manager
import json
import os

FILENAME = "notes.json"

# Load notes from file
def load_notes():
    if os.path.exists(FILENAME):
        with open(FILENAME, "r") as file:
            return json.load(file)
    return []

# Save notes to file
def save_notes(notes):
    with open(FILENAME, "w") as file:
        json.dump(notes, file, indent=4)

# Add a new note
def add_note(notes):
    title = input("Enter note title: ")
    content = input("Enter note content: ")
    note = {"title": title, "content": content}
    notes.append(note)
    save_notes(notes)
    print(" Note added successfully!\n")

# View all notes
def view_notes(notes):
    if not notes:
        print("No notes available.\n")
        return
    for index, note in enumerate(notes):
        print(f"\nNote {index + 1}")
        print(f"Title: {note['title']}")
        print(f"Content: {note['content']}")
    print()

# Search notes
def search_notes(notes):
    keyword = input("Enter keyword to search: ").lower()
    found = False
    for note in notes:
        if keyword in note["title"].lower() or keyword in note["content"].lower():
            print(f"\nTitle: {note['title']}")
            print(f"Content: {note['content']}")
            found = True
    if not found:
        print("No matching notes found.\n")

# Delete a note
def delete_note(notes):
    view_notes(notes)
    try:
        index = int(input("Enter note number to delete: ")) - 1
        if 0 <= index < len(notes):
            deleted = notes.pop(index)
            save_notes(notes)
            print(f" Deleted note: {deleted['title']}\n")
        else:
            print("Invalid note number.\n")
    except ValueError:
        print("Please enter a valid number.\n")

# Main menu
def main():
    notes = load_notes()
    while True:
        print("=== Personal Note Manager ===")
        print("1. Add Note")
        print("2. View Notes")
        print("3. Search Notes")
        print("4. Delete Note")
        print("5. Exit")
        
        choice = input("Choose an option (1-5): ")

        if choice == "1":
            add_note(notes)
        elif choice == "2":
            view_notes(notes)
        elif choice == "3":
            search_notes(notes)
        elif choice == "4":
            delete_note(notes)
        elif choice == "5":
            print("Goodbye! ")
            break
        else:
            print("Invalid choice. Please try again.\n")

if __name__ == "__main__":
    main()
