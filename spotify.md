# Spotify Architecture/tech stack
	https://www.quora.com/What-is-Spotifys-architecture/answer/Niklas-Gustavsson?ch=10&share=7207d9a4&srid=ueDOlA

	Spotify backend architecture is heavily service oriented. The backend is composed of about a hundred services, most of them fairly small and simple. Services are written in Python or Java with a few exceptions. 
	Services communicate primarily using our own protocol called Hermes, which is a message based and built on ZeroMQ and Protobuf. Older services still use HTTP and XML/JSON payloads. 
	Storage is primarily PostgreSQL, Cassandra or various static indexes. The latter primarily being used by the various content services, e.g. for search or metadata. 
	Audio files are stored in Amazon S3 and cached in our backend or using CDNs for low latency.

	The various clients keeps a persistent connection to a backend service called "accesspoint". It basically works as a messages router on steroids, handling communication with the needed services. 
	The protocol between clients and the accesspoint is proprietary.

	Clients for desktop, mobiles and our embeddable library, libspotify, all share a common code base. Each client then builds on this core to provide user interfaces and other platform specific adoptions. 
	The shared code base is written in C++ and the platform adoptions in the platform native languages, e.g. 

	ObjC on iOS. Also, many views and apps in the desktop client are now implemented as web apps, using an embedded instance of Chromium. Audio is retrieved from local cache, peer-to-peer or from our storage. Our P2P solution has been described in detail in various papers by Gunnar Kreitz (papers).
	Infrastructure is heavily based on Debian and open source software in general.