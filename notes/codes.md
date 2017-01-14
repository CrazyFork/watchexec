08d21a6dad4148e0b32baff16d90ddc645e35757

    // create a debounce
    fn wait(rx: &Receiver<Event>) -> Result<Event, RecvError> {

        let e = try!(rx.recv()); // recv block current thread

        // wait 250 milisecs first, then decide how to handle this .
        thread::sleep(time::Duration::from_millis(250));

        loop {
            /*
            RecvError:
                The recv operation can only fail if the sending half of a channel 
                is disconnected, implying that no further messages will ever be received.
            */
            match rx.try_recv() { // return immediately, without blocking
                Ok(_) => continue,// block on continuous receving
                Err(_) => break, // no more message.
            }
        }

        Ok(e)
    }



e01c45d6f549077d20383a317a2cc2c0f26647ae

    //file: Cargo.toml
    //more detailed way to specify dependency
    // see link: http://doc.crates.io/specifying-dependencies.html#choosing-features
    [dependencies.clap]
    version = "2.12.1"
    default-features = false
    features = ["wrap_help"]



153f0b0ed992ae74db08c1a983c8caf96063d40d

    /*
    grep version Cargo.toml
        #grep version keywork inside Cargo.toml
            result:
                version = "0.8.0"
                version = "2.12.1"
            
    head -n1 
        # only take the first line
        result:
            version = "0.8.0"

    grep -Eow '".+"'
        # only take the 0.8.0 part, 
            -E `extend regular expression`, 
            -o `only take matching group 0, the matching part`

    
    sed 's/"//g'
        # strip " 
    
    */
    VER=$(shell grep version Cargo.toml | head -n1 | grep -Eow '".+"' | sed 's/"//g')


    /*
    -c: create a archive
    -z: compress with gzip
    -C: change directory first
    */
    @tar -cz -C target/release -f target/release/watchexec_osx_$(VER).tar.gz watchexec


d087092f6419bdcff2019e2577c744c56f62ab59

    
    //file: filter.rs
    // rust string operations is quite peculiar
    // the feel on the code is quite bare metal
    // not like other language that make you feel you're simplely use string as an immutable data structure.
    pub fn add_extension(&mut self, extension: &str) -> Result<(), PatternError> {
        let mut pattern = String::new(); // create a string

        for ext in extension.split(",") {
            pattern.clear();    //clean on each loop
            pattern.push_str("*");

            if !ext.starts_with(".") {
                pattern.push_str(".");
            }
            pattern.push_str(ext);

            try!(self.add_filter(&pattern));// ref it. then mutate on another loop
        }

        Ok(())
    }

392aea8ca334595c1b220347a9048091c30d2163

    //crate version marcro

    #[macro_use]
    extern crate clap;

    .version(crate_version!())



