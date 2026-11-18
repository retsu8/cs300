William Paddock
CS 300 Module: Project One Milestone One

CLASS Course:
	VAR id = null
	VAR name = null
	VECTOR pre = vector<string> preReqs;

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

FUNCTION checkClassCourse():
	FOR (int c = 0; c < classList.size(); c++)
		COURSE course = classList[c]
		POINTER prereq => couse.pre
		BOOL found = FALSE
		FOR (int i = 0; i < prereq.size(); i++):
			INT itr = find(classHash.begin(), classHash.end(), prereq[i])
			IF(ITR == NULL):
				course.pre.erase(course.pre.begin() + itr)

FUNCTION search(course):
	INT count = 0
	FOR (string class: classHash):
		IF class == course:
			RETURN classList.at(count)
		++count
	RETURN null

FUNCTION printCourse(course):
	PRINT course.id + "  "
	PRINT course.name + "  "
	FOR (int i; i < course.pre; i++):
		PRINT course.pre[i]

vector<Course> = classList;
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