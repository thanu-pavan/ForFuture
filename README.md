# ForFuture

Chapter 2 Application Layer 


2.1 Principles of Network Applications 84
2.1.1 Network Application Architectures 86
2.1.2 Processes Communicating 88
2.1.3 Transport Services Available to Applications 91
2.1.4 Transport Services Provided by the Internet 93
2.1.5 Application-Layer Protocols 96
2.1.6 Network Applications Covered in This Book 97
2.2 The Web and HTTP 98
2.2.1 Overview of HTTP 98
2.2.2 Non-Persistent and Persistent Connections 100
2.2.3 HTTP Message Format 103
2.2.4 User-Server Interaction: Cookies 108
2.2.5 Web Caching 110
2.2.6 The Conditional GET 114
2.3 File Transfer: FTP 116
2.3.1 FTP Commands and Replies 118
2.4 Electronic Mail in the Internet 118
2.4.1 SMTP 121
2.4.2 Comparison with HTTP 124
2.4.3 Mail Message Format 125
2.4.4 Mail Access Protocols 125
2.5 DNS—The Internet’s Directory Service 130
2.5.1 Services Provided by DNS 131
2.5.2 Overview of How DNS Works 133
2.5.3 DNS Records and Messages 139
2.6 Peer-to-Peer Applications 144
2.6.1 P2P File Distribution 145
2.6.2 Distributed Hash Tables (DHTs) 151
2.7 Socket Programming: Creating Network Applications 156
2.7.1 Socket Programming with UDP 157
2.7.2 Socket Programming with TCP 163
2.8 Summary 168
Homework Problems and Questions 169
Socket Programming Assignments 179
Wireshark Labs: HTTP, DNS 181
Interview: Marc Andreessen 182

CHAPTER-02

*Application Layer*

Network applications are the raisons d’être of a computer network—if we couldn’t
conceive of any useful applications, there wouldn’t be any need for networking proto-
cols that support these applications. Since the Internet’s inception, numerous useful and
entertaining applications have indeed been created. These applications have been the
driving force behind the Internet’s success, motivating people in homes, schools, gov-
ernments, and businesses to make the Internet an integral part of their daily activities.
Internet applications include the classic text-based applications that became
popular in the 1970s and 1980s: text email, remote access to computers, file trans-
fers, and newsgroups. They include the killer application of the mid-1990s, the
World Wide Web, encompassing Web surfing, search, and electronic commerce.
They include instant messaging and P2P file sharing, the two killer applications
introduced at the end of the millennium. Since 2000, we have seen an explosion of
popular voice and video applications, including: voice-over-IP (VoIP) and video
conferencing over IP such as Skype; user-generated video distribution such as
YouTube; and movies on demand such as Netflix. During this same period we have
also seen the immergence of highly engaging multi-player online games, including
Second Life and World of Warcraft. And most recently, we have seen the emergence
of a new generation of social networking applications, such as Facebook and Twitter,
which have created engaging human networks on top of the Internet’s network of
routers and communication links. Clearly, there has been no slowing down of new
and exciting Internet applications. Perhaps some of the readers of this text will cre-
ate the next generation of killer Internet applications!
In this chapter we study the conceptual and implementation aspects of network
applications. We begin by defining key application-layer concepts, including network
services required by applications, clients and servers, processes, and transport-layer
interfaces. We examine several network applications in detail, including the Web,
e-mail, DNS, and peer-to-peer (P2P) file distribution (Chapter 8 focuses on multime-
dia applications, including streaming video and VoIP). We then cover network applica-
tion development, over both TCP and UDP. In particular, we study the socket API
and walk through some simple client-server applications in Python. We also provide
several fun and interesting socket programming assignments at the end of the chapter.
The application layer is a particularly good place to start our study of protocols.
It’s familiar ground. We’re acquainted with many of the applications that rely on the
protocols we’ll study. It will give us a good feel for what protocols are all about and
will introduce us to many of the same issues that we’ll see again when we study trans-
port, network, and link layer protocols.
2.1 Principles of Network Applications
Suppose you have an idea for a new network application. Perhaps this application
will be a great service to humanity, or will please your professor, or will bring you
great wealth, or will simply be fun to develop. Whatever the motivation may be, let’s
now examine how you transform the idea into a real-world network application.
At the core of network application development is writing programs that run on
different end systems and communicate with each other over the network. For
example, in the Web application there are two distinct programs that communicate
with each other: the browser program running in the user’s host (desktop, laptop,
tablet, smartphone, and so on); and the Web server program running in the Web
server host. As another example, in a P2P file-sharing system there is a program in
each host that participates in the file-sharing community. In this case, the programs
in the various hosts may be similar or identical.
Thus, when developing your new application, you need to write software that
will run on multiple end systems. This software could be written, for example, in C,
Java, or Python. Importantly, you do not need to write software that runs on network-
core devices, such as routers or link-layer switches. Even if you wanted to write
application software for these network-core devices, you wouldn’t be able to do so.
As we learned in Chapter 1, and as shown earlier in Figure 1.24, network-core
devices do not function at the application layer but instead function at lower layers—
specifically at the network layer and below. This basic design—namely, confining
application software to the end systems—as shown in Figure 2.1, has facilitated the
rapid development and deployment of a vast array of network applications.

