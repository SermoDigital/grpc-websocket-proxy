grpc-websocket-proxy
====================

[![GoDoc](https://godoc.org/github.com/tmc/grpc-websocket-proxy/wsproxy?status.svg)](http://godoc.org/github.com/tmc/grpc-websocket-proxy/wsproxy)

Wrap your grpc-gateway mux with this helper to expose streaming endpoints over websockets.

Usage:
```diff
	mux := runtime.NewServeMux()
	opts := []grpc.DialOption{grpc.WithInsecure()}
	if err := echoserver.RegisterEchoServiceHandlerFromEndpoint(ctx, mux, *grpcAddr, opts); err != nil {
		return err
	}
-	http.ListenAndServe(*httpAddr, mux)
+	http.ListenAndServe(*httpAddr, wsproxy.WebsocketProxy(mux))
```
