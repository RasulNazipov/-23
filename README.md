# -23
<!DOCTYPE html>
<html lang="en" ng-app>
<head>
  <meta charset="UTF-8">
  <title>СПИСОК ДЕЛ</title>
  <link rel="stylesheet" href="Case.css">
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.26/angular.js"></script>
  
</head>
<body>

  <h2>Список дел {{name}}</h2>

  Имя: <input type="text" ng-model="name"></br>
  
  <div ng-controller="CaseCtrl">
    <span>Всего {{Cases.length}} дел(а). Осталось {{remaining()}} дел(о)</span>
    <a href="" ng-click="delete()"><button>Удалить законченные дела</button></a>
    <a href="" ng-click="alldelete()"><button>Удалить все дела</button></a>
    
      <ul class="unstyled">
        <li ng-repeat="Case in Cases">
          <input type="checkbox" ng-model="Case.done">
          <span class="done-{{Case.done}}">{{Case.text}}</span>
        </li>
      </ul>
      <form ng-submit="addCase()">
        <input type="text" ng-model="CaseText"  size="20"
               placeholder="впишите новое дело">
        <input class="btn-primary" type="submit" value="Добавить">
        <input type="reset" value="Очистить"></p> 
        <a href="" ng-click="info()"><button>Хотите изменить?</button></a>

<script type="text/javascript">
function CaseCtrl($scope) {
  $scope.Cases = [
    {text:'Вынести мусор', done:true},
    {text:'Покормить коня', done:false}];
 
  $scope.addCase = function() {
    $scope.Cases.push({text:$scope.CaseText, done:false});
    $scope.CaseText = '';
  };


 
  
  $scope.remaining = function() {
    var count = 0;
    angular.forEach($scope.Cases, function(Case) {
      count += Case.done ? 0 : 1;
    });
    return count;
  };
 
  $scope.delete = function() {
    var oldCases = $scope.Cases;
    $scope.Cases = [];
    angular.forEach(oldCases, function(Case) {
      if (!Case.done) $scope.Cases.push(Case);
    });
  };

$scope.alldelete = function() {
    var alldelete = $scope.Cases;
    $scope.Cases = [];
  };

$scope.info = function() {
    var info = ('1) Выделите дело как законченное.\n2) Нажмите на кнопку "Удалить законченные дела" \n3) Добавте новое исправленное дело');
     
    alert(info);   
  };
  
}
</script>
<style type="text/css">
.done-true {
  text-decoration: line-through;
  color: red;
}
.done-false {
 color: green;
}
</style>
</body>

</html>
