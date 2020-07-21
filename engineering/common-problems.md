<!-- TITLE: Common Problems -->
<!-- SUBTITLE: Some common problems I deal with regularly that I always seem to forget the solution to -->

# Header
**Arrays in props** In componentDidUpdate(prevProps), the prevProps variable will be the same as this.props if the props have been mutated. This is common if the props has an array, such as metadata. The solution is to copy the array before any edits and reassign the props field with the edited copy. Places in the code where this may happen most include upsertDatum and creation of new listings. One occurrence was in new_listing.ts. The state variable was being mutated, so we added "const stateCopy = {...state};" and worked with stateCopy for the remainder of the function involved.![Screenshot From 2020 06 10 11 40 46](/uploads/screenshot-from-2020-06-10-11-40-46.png "Screenshot From 2020 06 10 11 40 46")

# not so common probs
this is where the not so common probs might happen

## docker-compose "No space left on device"
when trying to `docker-compose up` i gott an error `Cannot start service frontend: driver failed programming external connectivity on endpoint docker_frontend_1` and `Bind for 0.0.0.0:3000 failed: port is already allocated`
i checked if there was anything running on host with a `netcat command: nc -zv localhost 3000`  and it showed no processes running.
i tried to delete the network for `frontend` and purged older containers and images (`docker system purge`) and the problem persisted even though there was no process running on the host for port 3000.

docker-compose was just lying to me.

as i worked on testing a separate port for frontend, i ran into a problem building frontend in docker that had an error `No room left on device`

i then upped the amount of disk space for docker for mac (`Docker > Preference > Resources > Disk image size` from 65GB to 165GB) and both the "no space" and "port used" problems disappeared.