MiqroDB
=======

A useful class that helps you with querying MySQL in PHP easier.

----------

Examples
-------------
Create a table:

    $db = new MiqroDB(new MySQLi('localhost', 'root', 'user', 'password'));
    $db->createTable('users', [
	    'id' => [
		    'autoIncrement' => true,
		    'primary' => true
	    ],
	    'username' => [
		    'unique' => true,
		    'type' => 'varchar',
		    'length' => 255
	    ]
    ]);

Load data from the table:

	$entry = $db->table('users')->select('username', ['where' => 'id = 1'] )->getEntry(0);
	echo 'Username of user #1: ' . $entry['username'];

Insert into the table:

	$db->table('users')->insert([
		'id' => 2,
		'username' => 'john_smith99'
	]);
Insert a lot into the table:

	$db->table('users')->insertMany([
		['id' => 3, 'username' => 'daisy'],
		['id' => 4, 'username' => 'james_bond']
	]);
Build queries like PDO's prepared statements:

        $builder = new MiqroBuilder($db, 'INSERT INTO $table ( $fields ) VALUES ( $values )');
        $builder->set( 'table', 'users' );
        ...
        $builder->execute();
Check your query history:

        var_dump($db->getLastQueries());
And a lot of other cool functions. Check it out for yourself.
