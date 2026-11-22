William Paddock
CS 300 Module: Project One Milestone One

// Size is the same as the memory buffer
INT DEFAULT_SIZE = 128

STRUCT Class:
	STRING title
	STRING id
	vectore<string> prereq

CLASS HashCourse:
	private:
		STRUCT Node:
			Class class
			INT key
			NODE *next

			Node():
				key = UINT_MAX
				next = NULL
			
			Node(Class aClass) : Node():
				class = aClass

			Node(Class aClass, INT aKey) : Node(aClass):
				key = aKey
		
		vector<Node> nodes
		INT tableSize = DEFAULT_SIZE
		INT hash(INT key)

	public:
		HashTable()
		HashTable(INT size)
		virtual ~HashTable()
		VOID Insert(Class class)
		VOID PrintALL()
		VOID Remove(STRING classId)
		Class Search(STRING classId)
		size_t Size()

HashTable::HashTable()
	HashTable(DEFAULT_SIZE):

HashTable::HashTable(unsigned int size)
    : nodes(size EQUAL 0 ? DEFAULT_SIZE : size),
     tableSize(size EQUAL 0 ? DEFAULT_SIZE : size):

INT HashTable::hash(key):
	RETURN key % tableSize

HashTable::~HashTable():
    // erase nodes beginning
    FOR(Node& bucket: nodes):
        // Set next bucket for clearing
        Node* current = bucket.next

        WHILE(current NOT EQUAL nullptr):
            // Create the next node to store this node
            Node* next = current->next
            // Delete current node
            DELETE current
            current = next
        
        // Drop the bucket next pointer to clear the buckets list
        bucket.next = nullptr
        // Set the key back to the unit max to mark as empty
        bucket.key = UINT_MAX

HashTable::Insert(class):
    // create the key for the given class id
    // retrieve node using key
    SET INT idx TO hash(stoi(class.id))
    // Add or create a new node
    SET Node& bucket TO nodes[idx];
    // if no entry found for the key
    // assign this node to the key position
    IF ( CHECK bucket.key TO UINT_MAX){
        SET bucket.class TO class
        SET bucket.key TO idx
        RETURN
    }
    // running for loop while to append class if found
    SET Node* current TO &bucket
    WHILE(current-> next NOT EQUAL nullptr):
        SET current TO current -> next

    // Add a new node to the current bucket
    SET current -> next TO Node(class, idx)

FUNCTION processCSV(csvList):
	csv::Parser file = csv::Parser(csvPath); // read operations from stream
	
	TRY:
		FOR (int i = 0; i < file.rowCount(); i++):

            // initialize a bid using data from current row (i)
            CREATE Course course;
            SET course.id = file[i][0];
            SET course.name = file[i][1];

            // Start at 2 since we already know the first two; put the rest in a list
            // If there is no more than two, then we dont loop
            FOR (int j = 2; file[i].size; j++):
            	PUSH REQUIRED COURSE INTO course.pre from file[i][j]
            APPEND course to classList
            APPEND file[i][0] TO classHash

    CATCH (csv::Error &e):
    	// Check to make sure we have atleast 2 params, or the file[i][0] will fail
    	PRINT Error &e

void HashTable::Remove(string bidId):		
    // Look the buckets and check all nodes
    SET INT idx TO hash(stoi(bidId));
    SET Node& bucket TO nodes[idx];
    // Check to see if the bucket is empty        
    IF (bucket.key EQUAL UINT_MAX)
        RETURN // Bucket is empty

    // set the previus and current
    SET Node* previous TO nullptr
    SET Node* current TO &bucket

    // Set this to the next bucket temp to have a reference point for buckets
    SET Node* temp TO bucket.next

    // Use our tempt bucket to check if the head is what we want
    if (temp NOT EQUAL nullptr && temp->bid.bidId EQUAL bidId):
        // remove the bucket head
        SET bucket.next TO temp->next
        DELETE temp

    WHILE (current NOT EQUAL nullptr):
        IF (current->bid.bidId EQUAL bidId):
            // make sure previus already exists
            IF (previous NOT EQUAL nullptr):
                // Check and remove the found bid id
                SET previous->next TO current->next
                DELETE current
            BREAK

        // the previus to current and set current to next for next loop
        SETprevious TO current;
        SET current TO current->next

FUNCTION checkClassCourse():
	FOR (int c = 0; c < classList.size(); c++)
		COURSE course = classList[c]
		POINTER prereq => couse.pre
		BOOL found = FALSE
		FOR (int i = 0; i < prereq.size(); i++):
			INT itr = find(classHash.begin(), classHash.end(), prereq[i])
			IF(ITR == NULL):
				course.pre.erase(course.pre.begin() + itr)

Bid HashTable::Search(string bidId):
    // Search for the bidId
    Bid bid
    SET INT idx TO hash(stoi(bidId))
    SET Node& bucket TO nodes[idx]       
    SET Node* current TO &bucket
    WHILE(current NOT EQUAL nullptr):
        // find the bid in question
        IF (current -> bid.bidId EQUAL bidId){
            // Return the bid
            SET bid TO current -> bid
            BREAK
        SET current TO current -> next
    RETURN bid

FUNCTION printCourse(course):
	PRINT course.id + "  "
	PRINT course.name + "  "
	FOR (int i; i < course.pre; i++):
		PRINT course.pre[i]

vector<HashCourse> = classList;
vector<Course>::iterator courses;
vector<string> = classHash

FUNCTION menu:
	EXECUTE processCSV
	while choice != 9:
        PRINT "Menu:"
        PRINT "  1. Find Course"
        PRINT "  9. Exit"
        PRINT "Enter choice: "
        GET user input put in choice

      	SWITCH choice:
      		case 1:
      			PRINT "What course will we search?"
      			GET user input PUT into class
	            CLASS class = EXECUTE FUNCTION search(class)
	            EXECUTE FUNCTION printCourse(class)
	            break
	        default:
	        	PRINT "Choice not reconized"