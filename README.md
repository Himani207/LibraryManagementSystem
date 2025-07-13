import java.util.*;

public class LibraryManagement {
    static class Book {
        int id; String title, author; boolean issued;
        Book(int id, String t, String a){ this.id=id; title=t; author=a; issued=false; }
        public String toString() {
            return "["+id+"] "+title+" by "+author+(issued ? " (Issued)" : "");
        }
    }
    static class Member {
        int id; String name, email;
        Member(int i, String n, String e){ id=i; name=n; email=e; }
        public String toString() { return "["+id+"] "+name+" <"+email+">"; }
    }
    static class Library {
        Map<Integer,Book> books = new HashMap<>();
        Map<Integer,Member> members = new HashMap<>();

        void addBook(Book b) { books.put(b.id,b); System.out.println("Added: "+b);}
        void updateBook(int id, String newTitle) {
            Book b=books.get(id);
            if(b!=null){ b.title=newTitle; System.out.println("Updated: "+b);}
            else System.out.println("Book not found");
        }
        void deleteBook(int id) {
            Book b=books.remove(id);
            System.out.println(b==null?"Book not found":"Deleted: "+b);
        }
        void addMember(Member m) { members.put(m.id,m); System.out.println("Added: "+m);}
        void viewBooks() {
            if(books.isEmpty()) System.out.println("No books.");
            else books.values().forEach(System.out::println);
        }
        void searchBook(String key) {
            books.values().stream()
                    .filter(b->b.title.toLowerCase().contains(key.toLowerCase()))
                    .forEach(System.out::println);
        }
        void issueBook(int id) {
            Book b=books.get(id);
            if(b==null) System.out.println("Book not found");
            else if(b.issued) System.out.println("Book already issued");
            else { b.issued=true; System.out.println("Issued: "+b); }
        }
        void returnBook(int id) {
            Book b=books.get(id);
            if(b==null) System.out.println("Book not found");
            else if(!b.issued) System.out.println("Book not issued");
            else { b.issued=false; System.out.println("Returned: "+b);}
        }
        void sendEmailQuery(String email, String msg) {
            System.out.println("Email from "+email+": "+msg);
        }
    }

    public static void main(String[] args) {
        Library lib = new Library();

        // Admin adds books & members
        lib.addBook(new Book(1,"1984","George Orwell"));
        lib.addBook(new Book(2,"The Hobbit","J.R.R. Tolkien"));
        lib.addMember(new Member(1,"Alice","alice@example.com"));
        lib.addMember(new Member(2,"Bob","bob@example.com"));

        System.out.println("\n-- User Views Books --");
        lib.viewBooks();

        System.out.println("\n-- User Searches 'hobbit' --");
        lib.searchBook("hobbit");

        System.out.println("\n-- User Issues Book 2 --");
        lib.issueBook(2);

        System.out.println("\n-- User Returns Book 2 --");
        lib.returnBook(2);

        System.out.println("\n-- User Sends Email Query --");
        lib.sendEmailQuery("bob@example.com", "Please add more fantasy books.");

        System.out.println("\n-- Admin Updates Book 1 Title --");
        lib.updateBook(1, "Nineteen Eighty-Four");

        System.out.println("\n-- Admin Deletes Book 2 --");
        lib.deleteBook(2);

        System.out.println("\n-- User Views Books Again --");
        lib.viewBooks();
    }
}# LibraryManagementSystem
