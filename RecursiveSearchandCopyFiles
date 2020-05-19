function getSubFolders(parent, counter, sheet) {
  Logger.log("IN")
  counter=counter+1;
  
  var type =  'video/mp4' //add type 'video/quicktime','video/mp4','video/avi','video/mpeg'
  fileIter(parentFolder,sheet,type);

  parent = parent.getId();
  var folders = []
  var childFolder = DriveApp.getFolderById(parent).getFolders();
  while(childFolder.hasNext()) {
    var child = childFolder.next();
    folders.push(child);
    Logger.log(child.getName());
    counter = getSubFolders(child, counter, sheet);
  }
  return counter;
}


function fileIter(folder, sheet, type){
   var fileIt = folder.getFilesByType(type);
      while ( fileIt.hasNext() ) {
        Logger.log("HERE")
        var file = fileIt.next();
        Logger.log(file.getName());
        data = [
          file.getName(),
          folder.getName(), //folder name
          file.getDateCreated(),
          file.getSize(),
          file.getUrl(),
          "https://docs.google.com/uc?export=download&confirm=no_antivirus&id=" + file.getId(),
          file.getDescription(),
          file.getMimeType(),
        ];
        sheet.appendRow(data);
        var destFolderId = "1WPfzroyZSHsi8QTqf9rchhtQ6sUL7yZG";
        insertFileIntoFolder(folder,destFolderId, file);    
      }   
  
  
}
function insertFileIntoFolder(parent, folderId, file){
    var destination = DriveApp.getFolderById(folderId);
    file.makeCopy(destination);
    return;
  }

function Main() {
  var sheetname = "List of Files"
  var parentID = "1x14abW1ERjKZo1sjTsvWuixX-jfCPVGk"
  var sheet = SpreadsheetApp.create(sheetname);
  sheet.appendRow(["Name", "Folder", "Date", "Size", "URL", "Download", "Description", "Type"]);  //https://gist.github.com/woodwardtw/0aa352d43e135baf76de
  var parentFolder = DriveApp.getFolderById(parentID);
  var childFolders = parentFolder.getFolders();
  var counter = 0;
  var type =  'video/mp4'                        //add type 'video/quicktime','video/mp4','video/avi','video/mpeg'
  fileIter(parentFolder,sheet,type);

  while(childFolders.hasNext()) {
    var child = childFolders.next();
    Logger.log(child.getName());
    counter = getSubFolders(child, counter, sheet);
    Logger.log("counter");
    Logger.log(counter);
  }
  

}
