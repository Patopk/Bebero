library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity bebedero is
	Port (
		inicio: in std_logic;
		ck: in std_logic;
		E0: in std_logic;
		E1: in std_logic;
		S0: out std_logic;
		S1: out std_logic
		);
end bebedero;

architecture behavioral of bebedero is

type nombres_estados is (E0, E1, E2, E3);
signal estado: nombres_estados;
signal entrada_aux: std_logic_vector (1 downto 0);

begin

entrada_aux<=E0&E1;

process(inicio, ck)
begin
if inicio='1' then
	estado<=E0;
elsif ck='1' and ck'event then
	case estado is
		when E0 =>
			case entrada_aux is
				when "00" => estado<=E0;
				when "01" => estado<=E3;
				when "10" => estado<=E0;
				when "11" => estado<=E1;
				when others => estado<=E0;
			end case;
		when E1 =>
			case entrada_aux is
				when "00" => estado<=E3;
				when "01" => estado<=E3;
				when "10" => estado<=E2;
				when "11" => estado<=E1;
				when others => estado<=E0;
			end case;
		when E2 =>
			case entrada_aux is
				when "00" => estado<=E3;
				when "01" => estado<=E3;
				when "10" => estado<=E2;
				when "11" => estado<=E1;
				when others => estado<=E0;
			end case;
		when E3 =>
			case entrada_aux is
				when "00" => estado<=E3;
				when "01" => estado<=E3;
				when "10" => estado<=E2;
				when "11" => estado<=E1;
				when others => estado<=E0;
			end case;
		when others => estado<=E0;
	end case;
end if;
end process;

process(estado)
begin
case estado is
	when E0 =>
		S0<='0';
		S1<='1';
	when E1 =>
		S0<='0';
		S1<='0';
	when E2 =>
		S0<='0';
		S1<='1';
	when E3 =>
		S0<='1';
		S1<='0';
end case;
end process;

end behavioral;
