# Blowfish Algorithm


$key	=	'MySecureKey';	
$string	=	'user_id|||EMAIL|||ETC';	


	function Encrypt($string, $key) {
		$dirty = array("+", "/", "=");
		$clean = array("_PLUS_", "_SLASH_", "_EQUALS_");
		$result = '';
		for($i=0; $i<strlen($string); $i++) {
			$char = substr($string, $i, 1);
			$keychar = substr($key, ($i % strlen($key))-1, 1);
			$char = chr(ord($char)+ord($keychar));
			$result.=$char;
		}		
		$encrypted_string = base64_encode($result);			
		$encrypted_string = str_replace($dirty, $clean, $encrypted_string);
		return urlencode($encrypted_string);
	}
	
	function Decrypt($string, $key) {
		$dirty = array("+", "/", "=");
		$clean = array("_PLUS_", "_SLASH_", "_EQUALS_");
		$result = '';
		$string = urldecode($string);
		$string = str_replace($clean, $dirty, $string);	
		$string = base64_decode($string);		
		for($i=0; $i<strlen($string); $i++) {
			$char = substr($string, $i, 1);
			$keychar = substr($key, ($i % strlen($key))-1, 1);
			$char = chr(ord($char)-ord($keychar));
			$result.=$char;
		}		
		return $result;
	}
        
