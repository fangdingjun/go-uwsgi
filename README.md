go-uwsgi
=======

go-uwsgi implements a uwsgi server and a uwsgi client


##server example

		l, err = net.Listen("unix", "/path/to/socket")
		http.Serve(&go-wsgi.Listener{l}, http.HandlerFunc(func(w http.ResponseWriter, req *http.Request) {
			w.Header().Set("Content-Length", 11)
			w.Write([]byte("hello world"))
		})

this listen uwsgi at a unix socket, return a "hello world" response when there is a request

###client example

		l, err = net.Listen("tcp", ":4000")
        passenger := &go-uwsgi.Passenger("unix", "/path/to/socket")
        handler := http.HandlerFunc(func(res http.ResponseWriter, req *http.Request) {
            passenger.ServeHTTP(res, req)
        })
        server := &http.Server{Handler: handler}
        server.Serve(l)

this connects to the uwsgi unix socket and pass the request to it when there is a http request at port 4000 
