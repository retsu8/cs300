William Paddock
CS 300 Module: Project One Milestone One

vector<ClassCourse> = classList;

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
            FOR (int j = 2; file[i].size; j++):
            	PUSH REQUIRED COURSE INTO course.pre from file[i][j]
            APPEND course to classList

    CATCH (csv::Error &e):
    	// Check to make sure we have atleast 2 params, or the file[i][0] will fail
    	PRINT Error &e

FUNCTION checkClassCourse():
	

